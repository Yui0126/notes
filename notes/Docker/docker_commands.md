

### Database

To list all the databases in docker
```
docker compose exec db psql -U postgres -c "\l"
```

Enter into the database
```
docker compose exec db psql -U postgres -d consulchat_db_development
```
Routes
first, `docker compose exec web bash`
then,`bin/rails routes`


