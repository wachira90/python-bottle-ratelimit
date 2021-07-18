# python-bottle-ratelimit
python-bottle-ratelimit

## flask_limiter library to provide rate limiting features in our flask app. Following the
### https://flask-limiter.readthedocs.io/en/stable/

```
from flask_limiter import Limiter
from flask_limiter.util import get_remote_address
```

## After those imports, you will need to add a default limiter. Use this code snippet below.

```
limiter = Limiter(
    application,
    key_func=get_remote_address,
    default_limits=["200 per day", "50 per hour"]
)
```


## Each route you can individually customize the request limits and it will bypass the default limits.

```
# example 5 per minute route 
@application.route("/slow")
@limiter.limit("5 per minute")
def slow():
    return "5 per minute!"
```

## We can also exempt a route from the default limit and users will have unlimited access to that route.

```
# example no limit route
@application.route("/exempt")
@limiter.exempt
def exempt():
    return "No limits!"
```

## Rate Limit String Notation
### Example:

```
10 per minute
10 per hour
10/hour
10/hour;100/day;2000 per year
100/day, 500/7days
100/day, 500/7days
```
