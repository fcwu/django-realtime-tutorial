django-realtime-tutorial
========================

Copy from http://maxburstein.com/blog/realtime-django-using-nodejs-and-socketio/

```
#https://docs.djangoproject.com/en/dev/topics/install/
sudo apt-get install python-pip
sudo pip install django
   
#http://redis.io/download
sudo apt-get install redis-server
     
#https://github.com/andymccurdy/redis-py
sudo pip install redis
#https://github.com/joyent/node/wiki/Installing-Node.js-via-package-manager
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
     
#https://github.com/LearnBoost/socket.io
npm install socket.io
     
#https://github.com/shtylman/node-cookie
npm install cookie
```

Running
```
python manage.py syncdb
python manage.py createsuperuser
python manage.py runserver localhost:3000
cd nodejs && node chat.js
```


Code flow
---------

send message
```
YOU -> index.html ---------------------> chat.js ------> views.py ------> redis 
                socket.emit("send_message")     django/node_api  channel/chat
                                                                  ------> sqlite
                                                                 create comment in table core_message
```

receive message
```
YOU -> index.html <---------- sqlite (at beginning)
                   core_messages
                  <---------- chat.js
                   subscribe/chat
```
