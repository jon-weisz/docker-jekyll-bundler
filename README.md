This project creates an image useful for developing Jekyll based websites that use Bundle based package distributions. 

# Usage

## Build a Local Server Image

Create a Dockerfile containing the following in the base directory of your Jekyll image. It must be the same directory that contains your Gemfile and Gemfile.lock.

	From jonweisz/jekyll-bundler:onbuild

This command will download the packages specified in the Gemfile. 
	
Then create the image using the usual command, replacing image name with the name you wish to use for your blog image:
	
	docker build -t $IMAGENAME .

## Using the image

To run the image, with LOCALHOSTNAME and PORT as the localhost URI and port number to serve the website from, respectively (i.e. LOCALHOSTNAME= and PORT=4000):

	docker run -t -i -p $LOCALHOSTNAME:$PORT:4000 -v $PWD:/src $IMAGENAME

The server should now be running, and it should be possible to direct a website to http://LOCALHOSTNAME:PORT to see it. 

## Caveats

* Omitting the "-t -i" flags will prohibit CTRL-C from terminating the server as normal. Without it, you will need to kill the ruby process externally to terminate the image. 
* Using only the "-t" flag will allow the CTRL-C flag to escape the command that launched the server, but it will not terminate the image. Attempting to run the command again will yield and error because the port in question will already be bound to the prior invocation of docker. 
	
