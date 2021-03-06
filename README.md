# Presence Light

Recently I decided I wanted to have a Smart Light in my office that showed what my Presence was in Microsoft Teams. With some help, I threw together a little POC and posted to Twitter

![Image of Yaktocat](/static/tweet.png)

I got enough interest that I decided to make it a little more robust, so here is a repo.

## Graph Api

The hardest part to getting this to work was figuring out the Graph Api stuff around getting a User's presence. The Graph Api recently exposed a [Presence Endpoint](https://docs.microsoft.com/en-us/graph/api/presence-get?view=graph-rest-beta&tabs=http) that facilitates this, but like all Graph stuff, you have to create a Azure Active Directory Application Registration that has the following scopes

- Presence.Read
- Presence.Read.All

This is only available on the /beta endpoint, so things might move around. Here is a good [repo](https://developer.microsoft.com/en-us/graph/blogs/announcing-30-days-of-microsoft-graph-blog-series/) (I stole code from it) that shows what you need to do to get AAD registration done, follow that.

## Phillips Hue

I already had a Phillips Hue bridge and bulb so I decided to stick with that. There is a good repo called [Q42.HueApi](https://github.com/Q42/Q42.HueApi) that makes working with the Hue Api easier in C#. You will need to register an app and get the IP Address of your Bridge, which you can do at [Phillips Hue Developer Center](https://developers.meethue.com/develop/get-started-2/).

## Putting all those keys to use

Now that you have the AAD stuff and Phillips Hue Stuff, put it into your appsettings.json in this repo, like this.

```json
  "AppSettings": {
    "applicationId": "",
    "applicationSecret": "",
    "tenantId": "",
    "redirectUri": "",
    "domain": "",
    "hueIpAddress": "",
    "hueApiKey": ""
  }
```

If you have the right settings in there, and the right scopes, this code will work.

Right now, I have a .NET 3.1 Console App and an ASP.NET Core 3.1 Worker Service that you can use (I wanted to see how hard it was to do both) that leverage the same .NET Standard `Core` library that does all the lifting. In the future, I want to maybe configure the Worker to be a Windows Service or Linux Daemon (would be cool for a Pi Project) and maybe have a Desktop Client App.

## Please Contribute

If you want to contribute, please do, as this is not much more than a POC.


## Note to MSFT Employees

It was a pain to get the right access to use the Microsoft Tenant, if you want to use this code, please reach out to me.
