# Warning
This repository is being monitored by SourceGraph developers, so I do not have any guarantees or promises about this not breaking right away.
If they continue to change things around, I might stop updating sg-proxy altogether.

# Note
If you are ratelimited and want to check the ratelimit for your account, go to the [Cody chat](https://dereferer.me/?https%3A//sourcegraph.com/cody) and send a message. When over the limit, you should see an error like this:
>Request failed: you exceeded the rate limit for chat_completions, only 3 requests are allowed per day at the moment to ensure the service stays functional. Current usage: 3. Retry after 2023-09-06 <time> +0000 UTC


# sg-proxy - free Claude

Requirements: Node, NPM.

1) Create a SourceGraph account (no phone required, just normal email/password).
2) Go to https://sourcegraph.com/, click on your profile icon in upper-right, then Settings, then go to Account->Access tokens, and generate a new token.
3) Clone/download https://gitgud.io/cncanon/sg-proxy/.
4) Open `.env` in the proxy folder and put your token there, so it looks like `API_TOKEN="sgp_mytoken"`
5) Run `start.sh` if you're on *nix, otherwise run `start.bat`. If you want to run manually, just `npm install --no-audit` and then `node main.js`. 
6) Change completion to Claude in ST, set any API key, then set the proxy URL as `http://localhost:3000/v1` and set any password.

If you want to use it remotely, you can use any tunneling service e.g. ngrok or cloudflared, for example just `cloudflared tunnel --url http://localhost:3000` is enough to tunnel the proxy through Cloudflare, then you can access it via the given URL with the /v1 suffix.

Enjoy.

### Updates
- 04/09/2023 - Fixed getting 403 on completion requests - seems like SourceGraph started checking for some additional headers, not a big deal. 
- 30/08/2023 - Fixed two reported issues - [broken streaming for multi-byte characters (non-English text)](https://gitgud.io/cncanon/sg-proxy/-/issues/2) and [misleading error for when there's an error](https://gitgud.io/cncanon/sg-proxy/-/issues/1). Now you should be able to stream non-English text (Japanese, Russian, etc) and, if sg-proxy catches an error, see the note about it in the message instead of ST never finishing the request. 

### Notes
- Only tested with the model `claude-2`, older ones might work if their API allows to, maybe not.
- The upper limit on the context size is unknown, please test. The initial value was at ~20K, but that was due to a (fixed) bug in the proxy. Some people have reported being able to use 50-80K context without issues.
- The API has a daily rate-limit for requests. Some people have reported it as being at 100 requests, some - 50, but it might differ per-account. If you get a 429 error in console, just create a new account.

Contact: cncanon1@proton.me.
