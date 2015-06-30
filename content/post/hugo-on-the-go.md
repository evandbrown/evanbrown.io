+++
comments = true
date = "2015-06-30T00:00:00-00:00"
draft = false 
share = false 
image = ""
slug = "hugo-on-the-go"
tags = ["dev", "golang"]
title = "Hugo on the Go: Static Blogging from an iPhone"
+++

I moved from Ghost to [Hugo](http://gohugo.io) a few weeks ago. After ironing out a few kinks with look and feel, the only missing link was writing and publishing from my iPhone. Definitely not something I do often, but it was easy on Ghost and I thought it should at least be possible with Hugo.
<!--more-->
## Write and Publish from Workstation
Writing and publishing from a workstation with Hugo is pretty standard if you've used a static website/blog generator (like [Pelican](http://getpelican.com) or [Jekyll](http://jekyllrb.com/)). Here's my basic workflow to create and publish a new post from my laptop:

1. The site (minus the generated content) is on GitHub: [https://github.com/evandbrown/evanbrown.io](https://github.com/evandbrown/evanbrown.io)

1. Create a new post:

    ```shell
    hugo new -t casper post/probably-a-pizza-review.md
    ```

1. If there are images, they probably came from my phone and are synced to Dropbox, so I'll copy them into the blog:

    ```shell
    cp ~/Dropbox/camera-uploads/pizza-pic.jpg ~/dev/evanbrown.io/static/img/
    ```

1. Run the Hugo server and make sure things look good locally:

    ```shell
    hugo server -t casper
    ```

1. Looks good. I'll commit and push the changes:

    ```shell
    git add content/post/probably-a-pizza-review.md
    git add static/img/pizza-pic.jpg
    git commit -m "New Pizza Review"
    git push origin master
    ```

1. Finally, generate the static content and sync to S3:

    ```shell
    hugo -t casper
    aws --region us-west-2 s3 sync --recursive ~/dev/evanbrown.io/public/ s3://evanbrown.io/
    ```

It looks a lot worse than it is. Even if I wasn't worried about mobile, that last step where the site is generated and synchronized to S3 should be automated. Pushing to remote should be the final step in publishing, and as it turns out is the key piece in getting this to work on mobile.

## Authoring with Hugo on an iPhone
I knew there were two tools I needed to get this working:

1. **A git client for iOS** - I wasn't sure this existed, but it does. It's called [Working Copy](http://workingcopyapp.com/) and it is _bad ass_. Like, not just "it works, but it's a real pain-in-the-ass" functional, but actually fully-featured and easy to use. More on Working Copy below. It's $10. You should buy it.
1. [Travis](http://travis-ci.org) to generate the static site and push to S3 after it's been commited to GitHub. Like I said, automatic build and deploy is a huge win even if never publish from a phone. Travis is awesome and makes this trivial; details on the configuration below.

### Writing a Post with Working Copy
Since I don't have `hugo new...` on the phone, I created a template in `evanbrown.io/content/post/template.md` that I copy to a new file and start a new post. In addition to doing all of the git tricks, Working Copy also has a totally functional text editor, so I use it to write. Here's the basic flow, followed by a gif showing the UI:

1. Initial setup of Working Copy: sign into [GitHub](http://www.github.com) (or [BitBucket](http://www.bitbucket.com)) and you'll get a list of repositories to clone
1. In Working Copy, locate `template.md` and copy it to `new-post.md`
1. Open `new-post.md` in the Working Copy editor, change the front matter and write the post
1. If you have a photo, open Photos and send the picture to Working Copy. **I can't overstate this:** Working Copy has fantastic integration with iOS. It's trivial to sling or squirt or whatever files from an app into a git repo.
1. If you added a pic, now you have 2 files to commit. Write a commit message, then commit and push the files to GitHub.

Here's a gif showing all of that, plus a few meta frames showing creation of the gif and adding it to the repo, and finally committing/pushing the whole thing:

![](/img/hugo-init.gif)

### Build and Publish with Travis
I dropped a standard and simple `.travis.yml` in my repo. The current version is at [https://github.com/evandbrown/evanbrown.io/blob/master/.travis.yml](https://github.com/evandbrown/evanbrown.io/blob/master/.travis.yml). Here's a pretty snippet current as of the publishing date:

{{< highlight yaml "style=friendly" >}}
language: go
go:
- 1.4
install:
- go get github.com/spf13/hugo
script: hugo -t casper
deploy:
  provider: s3
  access_key_id: $AWS_ACCESS_KEY
  secret_access_key: $AWS_SECRET_KEY
  bucket: evanbrown.io
  region: us-west-2
  endpoint: evanbrown.io.s3-website-us-west-2.amazonaws.com
  local-dir: public
  skip_cleanup: true
  on:
    repo: evandbrown/evanbrown.io
{{< /highlight >}}

Again, Travis is badass. Combined with go binaries, this was so easy. We just `go get` hugo and override the build command with `script: hugo -t casper`. That generates the static content and puts it in the `public/` directory (relative to the build).

Travis provides built-in support for deploying to S3 after a build. This was the trickiest part. Set the `region` and `endpoint` to the correct values for your bucket. `skip_cleanup` is required so the generated files aren't deleted, and `local_dir` limits the uploaded files to those in the `public/` dir. Finally (and **most importantly**) I created an IAM user just for Travis, with s3::PubObject** just for my bucket:

{{< highlight json "style=friendly" >}}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "travis-put",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:PutObjectAcl",
                "s3:PutObjectVersionAcl"
            ],
            "Resource": [
                "arn:aws:s3:::evanbrown.io/*"
            ]
        }
    ]
}
{{< /highlight >}}

Copy and paste the values into `AWS_ACCESS_KEY` and `AWS_SECRET_KEY` env vars in Travis. Don't download or save the creds. Replace them in the future if you need to.

![](/img/travis-env.png)

Now I can push (from my workstation or iPhone), and Travis builds and publishes [http://evanbrown.io](http://evanbrown.io). And it costs like a few pennies a month, but I didn't switch from Ghost for that reason (I switched because I didn't want to manage upgrading the Ghost software and OS it ran on. Ain't got time for that.)

Here's a successful build:

![](/img/travis-build.png)

## Next Steps
Here's what I want to do next:

1. Get `www.evanbrown.io` to redirect to `evanbrown.io`
1. Put SSL on it
1. Create a `preview` branch that Travis builds and publishes to `preview.evanbrown.io` so I can...preview stuff before merging to `master` and pushing that? Nah, that sounds like overkill. Nevermind.
