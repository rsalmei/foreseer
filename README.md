# foreseer

A Rust weather cache service for playing with axum and Redis.

## Objective

I've been using Rust since 2020, but, curiously, all the companies I've worked for have used [warp](https://github.com/seanmonstar/warp) for their web servers. So, I wanted to try [axum](https://github.com/tokio-rs/axum), which seems like the best Rust web framework nowadays.

This is a simple service that allows you to retrieve weather forecasts for some cities, and automatically refresh them every few minutes. It keeps historical data on Redis with persistence, and allows you to control the background tasks' state, like pausing, resuming, changing the frequency, etc.

I'll use the [Open-Meteo API](https://open-meteo.com) to get the weather data, which offers a generous 10,000 free requests per day.
