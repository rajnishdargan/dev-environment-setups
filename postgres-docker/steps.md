# ✅ 1️⃣ Check your docker-compose.yml
## Open it and confirm:
```
environment:
  POSTGRES_USER: postgres
  POSTGRES_PASSWORD: postgres
  POSTGRES_DB: beneficiarydb
```
  
# ✅ 2️⃣ Stop and remove old container + volume (this is critical)
## Stop & remove container + volume
```
docker-compose down -v
```
This deletes the old database and ensures the next up creates a clean container with the correct postgres user.

# ✅ 3️⃣ Start fresh
```
docker-compose up -d
```

## ✅ Now this container will have:
```
User: postgres
Password: postgres
Database: beneficiarydb
```

# ✅ 4️⃣ Confirm the user exists
Check users:
```
docker exec -it my_postgres psql -U postgres -d beneficiarydb -c "\du"
```

You should see:
```
 Role name |                         Attributes                         | Member of 
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}
```

# ✅ 5️⃣ Now copy and import your SQL file
```
docker cp beneficiary-backend.sql my_postgres:/beneficiary-backend.sql
docker exec -it my_postgres psql -U postgres -d beneficiarydb -f /beneficiary-backend.sql
```
✅ This time it will work cleanly.

# ✅ Final check
List tables:
```
docker exec -it my_postgres psql -U postgres -d beneficiarydb -c "\dt"
```


