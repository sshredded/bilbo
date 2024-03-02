# bilbo
baggins
github = resource "https://api.github.com/",
  repo: (resource) ->
    resource "repos/{owner}/{repo}/",
      issues: (resource) ->
        resource "issues",
          create:
            method: "post"
            headers:
              accept: "application/vnd.github.v3.raw+json"
            expect: 201
          list:
            method: "get"
            headers:
              accept: "application/vnd.github.v3.raw+json"
            expect: 200

            try
  {data} = yield github
    .repo {owner, repo}
    .issues
    .list()
  console.log number, title for {number, title} in (yield data)
catch error
  console.error error
