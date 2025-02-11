
rebuild:
	docker compose --env-file=docker.env build --no-cache

up:
	docker compose --env-file=docker.env up -d

down:
	docker compose --env-file=docker.env down

shell:
	docker compose --env-file=docker.env exec  webserver su www-data -l -s /bin/bash