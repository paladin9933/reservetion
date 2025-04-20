## reservetion
#service for reservation tables in cafe


#install:
#if docker is already installed then that step you can skip


    for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg

    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    echo   "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
    "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

#install docker
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

#download the archive on any located forexample on profile path /home/username/
#expact the archive that place, forexample most be /home/username/project/<project's files>
 
#call a cd comand in CMD to set path
#forexample:
  cd /home/username/project
#first you need to add your ip addres in ALLOWED_HOSTS ./Django_RezerveTables/Django_RezerveTables/setting.py 
#and chenge server_name in ./default.conf.template you may set ip or set doman 

#next step made compose, for that tab in command lite this command:
  docker compose up -d

#wait until bilding complit

#if needed update migration call: 
    sudo docker exec -it project-web-1 python /code/manage.py makemigrations
    sudo docker exec -it project-web-1 python /code/manage.py migrate 

#USE tables

#  use the GET request and url http://your_host:80/app/table/  for get all tables

#  use the DELETE request and url http://your_host:80/app/table/create/<id> for delete the table from database where id - table's id

#  use the POST request and url http://your_host:80/app/table/create/ for add the new table. the post request must have the new table's data, 
#  {"name": "table's name", "seats":"number, how muth person can seats", "location":"table's location"}, for example { "name":"table 1", "seats": 4, "location":"the table is nearby the window" }

#USE reservation

 #   use the GET request with key rezerv=True and url http://your_host:80/app/reserve/  for get all tables, forexample http://your_host:80/app/reserve/?rezerv=True

#    use the DELETE request and url http://your_host:80/app/reserve/<id> for delete the reserve from database where id - reserve's id

#    use the POST request and url http://your_host:80/app/table/create/ for add the new reserve. the post request must have the new reserve's data,
#    {  "customer_name": "costomer's name","table_id": "table's id who get reservation", "reservation_time": "date and time reservation in format YYYY-MM-DDThh:mm:ss+UTC", "duration_minutes": minuts how long will be reservation }  forexample  { "customer_name": "Джонни Си", "table_id": "3", "reservation_time": "2025-04-19T06:30:00+10:00", "duration_minutes": 60 } 
#    if the post request will be susses you get answer with your request reservation else you get error answer for example you try made reservation on table who already have reservation on this time or you lost any fild in reques 
    


  

    
