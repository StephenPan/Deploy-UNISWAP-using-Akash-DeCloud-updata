## Deploy UNISWAP using Akash DeCloud

### Akash, go, go, go, go, go。。。。



Although we have published the relevant content, but I am not very satisfied, so today to re-release a detailed and accurate deployment strategy, I hope you like.









Before we get started, a word about Akash in passing.



Phase 3 will accelerate our vision for a decentralized and open cloud computing marketplace and serve as the launchpad for Mainnet 2. 

#### **Rewards** **_____**

You can check out [The Akashian Challenge site](https://akash.network/challenge/) for a detailed schedule of reward opportunities. A total of **500,000 AKT** is allocated for Phase 3 Rewards including:

1. **Guided Challenges**
2. **Open Ended Challenges**
3. **Network Support Challenges**
4. **Community Content Challenges**
5. **Bonus Challenges**



#### **This Week’s Live Stream on Friday _____**

Don’t miss our weekly Phase 3 live stream this Friday December 11th at 9am PST / 5pm UTC, featuring our CEO Greg Osuri and CTO Adam Bozanich, and hosted by Michael Gushansky, our Senior Global MarComm Manager.

We’ll have exclusive updates, a Q&A, and special prizes. 



#### **Don’t Miss the Latest Phase 3 Updates**

For more information about Akash, please use the following links to learn more.

Official Website: https://akash.network/?lang=zh-hans

Twitter: https://twitter.com/akashnet_

Telegram: https://t.me/AkashNW

















## About Docker



For those unfamiliar with Docker, it is highly recommended to take a look at the 30 minute quick start Docker tutorial (https://juejin.cn/post/6844903815729119245) , install it locally and run it.



The following terms are image and container



\* * * Mirror * * You can think of it as a pre installed Linux distribution, just as you can rent VPS with Ubuntu or Centos, with different programs on different systems. You can download images from a Dockerhub, or you can create your own.



\* * Container * * Is An instance of a mirror that can be used to change directories, modify files, run scripts, and so on, just like with a Linux server.



Unlike a real virtual machine, docker’s lower level is interoperable and lightweight. The smallest mirror, Alpine, is less than 6 mb.



### Deploy Uniswap

First, we need to prepare a Docker image according to Akash’s official [ deployment tutorial ](Url) . For simple installation and use of Docker, refer to my previous [ simple tutorial ](https://www.jianshu.com/p/2614faa56cf6) .。

**\* Compiler applications * ***

>  You can skip this step if you already have a Docker image of UNISWAP.
>
> 
>
> First pull up the latest code from the https://github.com/Uniswap/Uniswap-interface
>
> 
>
> \```
>
> git clone https://github.com/Uniswap/uniswap-interface.git
>
> \```
>
> 
>
> Pull to complete as follows
>
> 
>
> \```
>
> ➜ github git clone https://github.com/Uniswap/uniswap-interface.git
>
> Cloning into 'uniswap-interface'...
>
> remote: Enumerating objects: 10317, done.
>
> remote: Total 10317 (delta 0), reused 0 (delta 0), pack-reused 10317
>
> Receiving objects: 100% (10317/10317), 16.39 MiB | 5.88 MiB/s, done.
>
> Resolving deltas: 100% (6171/6171), done.
>
> \```
>
> 
>
> Then go to the UNISWAP directory
>
> 
>
> \```
>
> cd uniswap-interface
>
> \```
>
> 
>
> INSTALLATION DEPENDENCY
>
> 
>
> \```
>
> yarn
>
> \```
>
> 
>
> Note: If this step prompts you for ‘command not found: Yarn’ , you need to install ‘yarn’ first, using the command
>
> \>
>
> \> ```brew install yarn
>
> \> brew install yarn
>
> \> ```
>
> 
>
> Launch Application
>
> 
>
> \```
>
> yarn start
>
> \```
>
> 
>
> After successful launch, you can access Uniswap via http://localhost:3000 in your browser window.
>
> 
>
> We then package the application with the ‘yarn build’ command
>
> 
>
> \```
>
> ➜ uniswap-interface git:(master) yarn build
>
> yarn run v1.22.10
>
> $ react-scripts build
>
> Creating an optimized production build...
>
> Compiled successfully.
>
> 
>
> File sizes after gzip:
>
> 
>
> 626.67 KB build/static/js/4.27376761.chunk.js
>
> 245.71 KB build/static/js/5.44975b0b.chunk.js
>
> 185.08 KB build/static/js/9.c6fffc81.chunk.js
>
> 125.35 KB build/static/js/main.d38f6656.chunk.js
>
> 70.25 KB build/static/js/6.247f4f12.chunk.js
>
> 62.43 KB build/static/js/0.454e5a78.chunk.js
>
> 6.56 KB build/static/js/1.ab9e1769.chunk.js
>
> 1.24 KB build/static/js/runtime-main.d9a528e1.js
>
> 913 B build/static/css/4.f04942fe.chunk.css
>
> 166 B build/static/js/7.be8c5419.chunk.js
>
> 165 B build/static/js/8.9b1dfb7e.chunk.js
>
> 
>
> The project was built assuming it is hosted at ./.
>
> You can control this with the homepage field in your package.json.
>
> 
>
> The build folder is ready to be deployed.
>
> 
>
> Find out more about deployment here:
>
> 
>
> bit.ly/CRA-deploy
>
> 
>
> ✨ Done in 74.15s.
>
> \```
>
> 
>
> After successful packaging the file will be placed in the ‘. Directory.
>
> 
>
> \* * Make a Docker mirror * *
>
> 
>
> Now we need to create a Docker image using the newly packaged application. There are many ways to create a Docker image on the https://juejin.cn/post/6844903815729119245
>
> 
>
> Docker builds images in two ways, one using the ‘Docker build ‘command and the other using the ‘Docker build ‘command and the ‘Dockerfile’ file. The ‘docker commit ‘command is not recommended as it does not standardize the entire process, so it is more recommended to use the ‘docker build ‘command and the ‘Dockerfile’ file to build our image in the enterprise. We used ‘Dockerfile’ to make the build image more repeatable, while ensuring the standardization of the startup script and the running program.
>
> 
>
> Here we use the ‘docker build ‘command and the ‘Dockerfile’ file to build our mirror
>
> 
>
> First we create the ‘Dockerfile’ file via the command
>
> 
>
> \```
>
> vi Dockerfile
>
> \```
>
> 
>
> Fill it in
>
> 
>
> \```
>
> \# nginx as the base image
>
> FROM nginx
>
> \# since Uniswap is a standard web application, we copy the build directory into the nginx directory
>
> COPY build /usr/share/nginx/html
>
> \# flag that port 80 is running internally
>
> EXPOSE 80
>
> \# identifies the command to be executed when the container is started
>
> CMD ["nginx", "-g", "daemon off;"]
>
> \```
>
> 
>
> Once saved, execute the Docker command to package the image as ‘Docker build. - T UNISWAP: latest’
>
> 
>
> \```
>
> ➜ uniswap-interface git:(master) ✗ docker build . -t uniswap:latest
>
> [+] Building 18.1s (7/7) FINISHED
>
> => [internal] load .dockerignore 0.0s
>
> => => transferring context: 2B 0.0s
>
> => [internal] load build definition from Dockerfile









#### **This Week’s Live Stream on Friday _____**

Don’t miss our weekly Phase 3 live stream this Friday December 11th at 9am PST / 5pm UTC, featuring our CEO Greg Osuri and CTO Adam Bozanich, and hosted by Michael Gushansky, our Senior Global MarComm Manager.

We’ll have exclusive updates, a Q&A, and special prizes. 



#### **Don’t Miss the Latest Phase 3 Updates**

For more information about Akash, please use the following links to learn more.

Official Website: https://akash.network/?lang=zh-hans

Twitter: https://twitter.com/akashnet_

Telegram: https://t.me/AkashNW



