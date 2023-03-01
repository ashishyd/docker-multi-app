Dockerize mongodb, we expose port if backend is still not dockerize and not running in network

`docker run --name mongodb --rm -d -p 27017:27017  mongo`

Create docker container in network

`docker network create goals-net`

In frontend
`docker build -t goals-react .`

In backend
`docker build -t goals-node .`

Running containers, we utilize bind mount for live code changes in backend and frontend

`docker run --name goals-frontend -d --rm -p 3000:3000 -it -v /Users/ashishyd/Desktop/Development/playground/docker-multi-app/frontend/src:/app/src goals-react`

`docker run --name goals-backend -d --rm --network goals-net -p 80:80 -v /Users/ashishyd/Desktop/Development/playground/docker-multi-app/backend:/app -v logs:/app/logs -v /app/node_modules goals-node`

`docker run --name mongodb --rm -d --network goals-net -v data:/data/db mongo`
