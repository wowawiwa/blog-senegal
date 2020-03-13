A <a href="https://wowawiwa.github.io/senegal">blog about my travel in Senegal</a>.

## Processing pictures

I used `mogrify` command-line to generate the thumbnails or reduce the picture size:

```
mogrify -path ./img-thumbs -thumbnail x200 ./img-src/*.jpg
```

```
mogrify -resize 50% *.jpg
```

## Custom domain

### How to

The goal is to have `https://senegal.john.org` display the blog (without any additional path). I.e. `senegal` is the desired subdomain.

Assumptions:
- Your GitHub pages URL is `https://johnny.github.io/myblog`.
- You own `john.org`.

Generally, every change can take time. In my experience, operations are generally effective in less than 3 minutes. If something doesn't work, first give it a bit of time.

#### On the DNS Provider

Add the following record:
- Name: `senegal`
- Type: `CNAME`
- Data: `johnny.github.io`

With Google Domains, it's the _Custom resource records_ section of the _DNS_ config.

#### On GitHub repository settings

- Set the _Custom domain_ to `senegal.john.org`.
- Activate _Enforce HTTPS_ (could be available only after GitHub detected the custom domain has been properly configured).

### How it works

- The user request `senegal.john.org`.
- Because of the configured CNAME, the DNS request returns the IP of `johnny.github.io`, i.e. the IP of GitHub.
- GitHub receives a request with `senegal.john.org` and deduces which repo the request corresponds to using the _custom domain_. (It is unique accross GitHub. GitHub returns an error when trying to add twice the same _custom domain_ on two different repo.)
