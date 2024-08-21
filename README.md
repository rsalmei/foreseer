# foreseer

A Rust weather cache service for playing with axum and Redis.

## Objective

I've been using Rust since 2020, but, curiously, all the companies I've worked for have used [warp](https://github.com/seanmonstar/warp) for their web servers. So, I wanted to try [axum](https://github.com/tokio-rs/axum), which seems like the best Rust web framework nowadays.

This is a simple service that allows you to retrieve weather forecasts for some cities, and automatically refresh them every few minutes. It keeps historical data on Redis with persistence, and allows you to control the background tasks' state, like pausing, resuming, changing the frequency, etc.

I'll use the [Open-Meteo API](https://open-meteo.com) to get the weather data, which offers a generous 10,000 free requests per day.

## API

This is the simplest API I could think of, with only one resource. No /cities, no /tasks, just /weather.

```text
// CRUD.
GET /weather -> lists all cities
POST /weather -> creates new city (and associated background task)
GET /weather/<id> -> retrieves the details of one city
PUT /weather/<id> -> updates one city
DELETE /weather/<id> -> deletes one city (and associated background task)

// Weather functions.
GET /weather/today -> gets the current day forecast for all cities
GET /weather/tomorrow -> gets the next-day forecast for all cities
GET /weather/<id>/forecast -> gets a 7-day forecast for one city

// Background tasks functions.
GET /weather/tasks -> lists all background refresh tasks
GET /weather/tasks/active -> lists all active tasks
PUT /weather/tasks/<id> -> changes the frequency of one task
POST /weather/tasks/pause -> pauses all background tasks
POST /weather/tasks/resume -> resumes all background tasks
POST /weather/tasks/<id>/pause -> pauses one background task
POST /weather/tasks/<id>/resume -> resumes one background task
```

### Notes

There are no paginated responses for now, as well as any kind of historic data. But both could be added in the future.
