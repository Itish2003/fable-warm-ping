# fable-warm-ping

Keeps [fable20.vercel.app](https://fable20.vercel.app) warm.

fable ships google-adk (~573 MB installed), so a cold Vercel function takes
~7 s to answer its first request — long enough that the portfolio's 5 s
agent-card probe renders the leaf as offline on a cold first visit. Vercel
Hobby crons are daily-only, so an external pinger it is.

A scheduled GitHub Actions workflow curls the agent card every 5 minutes
(public repo → free unlimited Actions minutes):

- non-200 fails the run, so GitHub's failure email works as an uptime alert
- an empty keepalive commit lands every ~45 days, because GitHub disables
  schedules in repos with no activity for 60 days
