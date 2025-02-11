

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




Stop all the containers
```
docker stop $(docker ps -a -q)
```

`docker container prune`

To delete all containers including its volumes use,
`docker rm -vf $(docker ps -aq)`


To delete all the images,
`docker rmi -f $(docker images -aq)`

