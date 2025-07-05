# 📦 How to connect your Docker Postgres to pgAdmin

## ✅ 1️⃣ Open pgAdmin
Launch pgAdmin on your system.

## ✅ 2️⃣ Create a New Server connection
- In the pgAdmin browser panel, right-click on Servers
- Select Create → Server

## ✅ 3️⃣ Fill in connection details
In the dialog box:
General Tab:
- Name: Local Docker Postgres (or any name you like)

Connection Tab:
- Host name/address: localhost
- Port: 5432
- Maintenance database: beneficiarydb (or postgres — doesn't matter, you can switch after)
- Username: postgres
- Password: postgres (🔳 Optional: check Save Password)
Click Save


## ✅ 4️⃣ Verify the connection
- Expand the Databases section under your new server.
- You should see:
  - beneficiarydb
  - postgres
  - template0
  - template1
 
If you don't see beneficiarydb right away:
- Right-click on Databases
- Click Refresh

## ✅ 5️⃣ (Optional) Open beneficiarydb and check tables
Expand Databases → beneficiarydb → Schemas → public → Tables
You should see the tables you restored from your SQL dump
