######################
# Commands           #
######################

## Container Related Commands##

	$ docker run -i -t ubuntu /bin/bash  			# New instance from image
	$ docker ps						# List only active containers
	$ docker ps -a 						# List all containers

	$ docker stop [container-name|container-id]		# Stop a container
	$ docker stop -t1					# Stop a container (timeout = 1 second)

	$ docker rm [container-name|container-id] 		# Remove a stopped container
	$ docker rm -f [container-name|container-id] 	        # Force stop and remove a container
	$ docker rm -f $(docker ps-aq) 				# Remove all containers
	$ docker rm $(docker ps -q -f “status=exited”) 	 	# Remove all stopped containers

	$ docker exec -it [container-name|container-id] bash  	# Execute and access bash inside a container
	$ docker logs -f [container-name|container-id]        	# Instance console log
		
## Image Related Commands ##

	$ docker build -t [username/]<image-name>[:tag] <dockerfile-path>  	 #Build an image using a Dockerfile

	$ docker images 							 # List the images
	$ docker search <keyword>  						 # search images that matches the keyword
 
	$ docker rmi [username/]<image-name>[:tag]  				 #Remove an image from the local registry
		
	$ docker tag <image-name> <new-image-name>     				 # Creates a new image with the latest tag
	$ docker tag <image-name>[:tag][username/] <new-image-name>.[:new-tag]	 # Creates a new image specifying the “new tag” from an 										 # existing image and tag
		
	$ docker save -o <filename>.tar 					# Export the image to an external file
	$ docker load -i <filename>.tar 					# Import an image from an external file

	$ docker push [registry/][username/]<image-name>[:tag] Push an image to a registry
		
## Network related commands ##

## Volume related commands ##

## Other Commands ##

#######################
# Dockerfile          #
#######################
