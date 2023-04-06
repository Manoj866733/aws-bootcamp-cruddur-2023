# Week 4 — Postgres and RDS

## Provision RDS Instance
Create a RDS instance using AWS CLI

aws rds create-db-instance \
  --db-instance-identifier cruddur-db-instance \
  --db-instance-class db.t3.micro \
  --engine postgres \
  --engine-version  14.6 \
  --master-username root \
  --master-user-password huEE33z2Qvl383 \
  --allocated-storage 20 \
  --availability-zone ap-south-1a \
  --backup-retention-period 0 \
  --port 5432 \
  --no-multi-az \
  --db-name cruddur \
  --storage-type gp2 \
  --publicly-accessible \
  --storage-encrypted \
  --enable-performance-insights \
  --performance-insights-retention-period 7 \
  --no-deletion-protection
  
  


![Screenshot 2023-03-18 215116](https://user-images.githubusercontent.com/100923201/230331035-43a227e5-23a0-4de6-97cf-c5de5248029d.png)



![Screenshot 2023-03-20 141135](https://user-images.githubusercontent.com/100923201/230331293-3c07a438-2138-4c61-a7f4-e23c97a04b2a.png)


![Screenshot 2023-03-20 154615](https://user-images.githubusercontent.com/100923201/230331393-84259791-ec93-4752-859a-dd68f20d8ae5.png)


![Screenshot 2023-03-20 155719](https://user-images.githubusercontent.com/100923201/230331442-81f9d9e3-7c97-47a7-840b-a58b884cb20e.png)


![Screenshot 2023-03-20 224851](https://user-images.githubusercontent.com/100923201/230332047-98c416a6-5f67-42c3-9332-e14727107a5a.png)


![active connection](https://user-images.githubusercontent.com/100923201/230332154-92dda2c9-7417-46ad-809d-94dc0e55418a.png)


![Screenshot 2023-03-21 002705](https://user-images.githubusercontent.com/100923201/230332216-bd8f74f3-19f8-4dca-93e4-e9c7fe096c0e.png)


![Screenshot 2023-03-22 191637](https://user-images.githubusercontent.com/100923201/230332499-7c4c6794-e123-4c80-96fc-a9a887b923ab.png)


![Screenshot 2023-03-23 213937](https://user-images.githubusercontent.com/100923201/230332574-944ad7ef-722c-4262-a933-ea7c78c00097.png)


