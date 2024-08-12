# problem1DEPI
Step 1 :
Run an Nginx container named my-nginx and attach two volumes to the container:
    Volume1: For containing static HTML files.
    Volume2: For containing Nginx configuration files.
mkdir -p ~/nginx-html
mkdir -p ~/nginx-conf

Run the Nginx container with the volumes attached:
    docker run -d \
      --name my-nginx \
      -v ~/nginx-html:/usr/share/nginx/html \
      -v ~/nginx-conf:/etc/nginx/conf.d \
      nginx
      
------------------------------------------------------------------------------------------------------------------------------------
Step 2: 
Edit the HTML content
    Edit the index.html file located in ~/nginx-html:
echo "<h1>Hello from my-nginx container!</h1>" > ~/nginx-html/index.html

------------------------------------------------------------------------------------------------------------------------------------
Step 3: 
Remove the container ---------> Stop and remove the my-nginx container:
    docker stop my-nginx
    docker rm my-nginx
    
------------------------------------------------------------------------------------------------------------------------------------
Step 4: 
Run two new containers with the volumes attached in different ways
Container 1: 
Using Volume Mount --------> Run the first container using volume mount:
    docker run -d \
      --name my-nginx-volume-mount \
      -v ~/nginx-html:/usr/share/nginx/html \
      -v ~/nginx-conf:/etc/nginx/conf.d \
      -p 8080:80 \
      nginx

Container 2: 
Using Bind Mount -------> Run the second container using bind mount:
    docker run -d \
      --name my-nginx-bind-mount \
      -v $(pwd)/nginx-html:/usr/share/nginx/html:ro \
      -v $(pwd)/nginx-conf:/etc/nginx/conf.d:ro \
      -p 8081:80 \
      nginx
      
------------------------------------------------------------------------------------------------------------------------------------
Step 5:
Access the HTML files from your browser ------> Open your browser and go to:
        For Container 1: http://localhost:8080
        For Container 2: http://localhost:8081
