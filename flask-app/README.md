docker build -t <YOUR-USER>/firstapp .

docker run -p 8888:5000 --name firstapp YOUR_USERNAME/firstapp

docker login

docker push YOUR_USERNAME/firstapp

docker rm -f firstapp