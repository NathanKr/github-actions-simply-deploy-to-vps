<h1>todo - remove at end</h1>
<ul>
<li>where is this workflow ???? as template ?? </li>
</ul>


<h1>Project Name</h1>
Basic VPS deploy workflow using Github Actions

<h2>Project Description</h2>
Github actions workflow that clone private repo on VPS deploy folder. The prev deploy folder is renamed  

<h2>Motivation</h2>
You have a private repo on Github and you want to deploy it to VPS upon git post to main branch using a workflow file

<h2>Installation</h2>


<h3>Setup secrets.VPS_CICD_PRIVATE_KEY (once)</h3>
explain why this is needed !!!!!!!!!!!!!!!!

navigate to your repo setting and scroll down to 'Secrets and variables' as shown in the image

<img src='./figs/setting-secrets.png'>



<h2>Technologies Used</h2>
<ul>
<li>SSH</li>
<li>Public \ private key authentication (VPS)</li>
<li>Github Actions : workflow , secrets and GITHUB_TOKEN</li>
<li>act (not a success here)</li>
<li>Digital ocean droplet</li>
</ul>


<h2>Usage</h2>
Push to main branch


<h2>High level design</h2>
There are four components
<ul>
<li>your local machine - issue from here e.g. git push to main branch</li>
<li>Github - your private repo to be deployed on VPS is here</li>
<li>Github Actions Runner - this run the workflow file</li>
<li>VPS - here the private repo is deployed on digital ocean droplet</li>
</ul>

These four component and the flow between them is described in this image
<img src='./figs/high-level-schema.png'/>

<h2>Design</h2>

Following are questions that i have asked myself when starting this repo. After the repo is finish i have also the answewrs as listed here

<h3>Design question : should i use ssh agent</h3>
i see no benefit in my use case for ssh-agent

<h3>Design question : the repo is privte so how to access it</h3>
Using github actions the best solution is to use GITHUB_TOKEN .

<h3>Design question : how the VPS get the repo</h3>

<ol>
<li>clone by the VPS . runner need to copy GITHUB_TOKEN to the VPS</li>
<li>trnasfer from the runner to the VPS using ssh .runner use GITHUB_TOKEN and scp to copy the repo to the VPS</li>
</ol>



<h3>Design question : where to store VPS SSH private key so the runner can access it </h3>
The best solution to store screts in github is to use Github secrets which is part of the repo. And this is what i will use

<strong>which one to choose desktop \ laptop</strong>
It does not matter so i choose the cicd private key on the pc (\\wsl$\Ubuntu\home\nathan\.ssh\cicd_user_server_digital_ocean) for VPS_CICD_PRIVATE_KEY 

<h2>Code Structure</h2>
put here all workflow or part of it ???????
....

<h2>Demo</h2>
following push to main branch you can check the staus on github dashboard as shown in the following image

<img src='./figs/deploy-clone-success.png'/>

<h2>Points of Interest</h2>
<ul>
<li><strong>VPS ip in github actions secrets</strong>
Used like so just so it wont be expose to public yet work for the repo owner
</li>

<li><strong>Invoke parts of workflow using act</strong>
I am able to invoke specific job

```bash
        act -j deploy-clone
```

</li>
   
</ul>

<h2>Open issues</h2>
<ul>
<li>id_rsa is used in clone-repo-on-vps.yml even though the key is not rsa. otherwise i started getting issues. may be relating to default or ~ on VPS vs runner</li>
 <li>act did not finish the workflow clone-repo-on-vps.yml as shownin the following image
 
 <img src='./figs/act-fails.png'/>

 </li>
 <li>i am not able to invoke specific workflow. it is starting but hangs

```bash
    act -w .\.github\workflows\clone-repo-on-vps.yml
```   
</li>
</ul>

<h2>Possible improvments</h2>
<ul>
<li><strong>Eliminate copy GITHUB_TOKEN to VPS</strong>
There is some security risk here because the token is exposed on the VPS ,altough it is removed after the job is ended. You might eliminate this by maybe use scp and simply copy the repo from the runner to the VPS using scp 
</li>
<li><strong>Eliminate hard code DEPLOYMENT_DIR</strong>
possible solution is to use config file in the github actions level
</li>
<li><strong>Add specific project stuff to workflow</strong>
You might have packages you need to install , stop the app before deploy , restart it after deploy and alike. you can add all of this as bash code to the workflow file or add script and call it from the workflow. 
</li>
</ul>

<h2>References</h2>
<ul>
    <li><a href='https://www.youtube.com/watch?v=R48-UaZ4q1k'>SSH Essentials in 7.5 minutes </a></li>
    <li><a href='https://youtu.be/x239z6DdE0A?si=Di81DK0RrphVxkmZ'>Introduction to GitHub Actions: Learn Workflows with Examples</a></li>
    <li><a href='https://youtu.be/Mir-uLSQmwA?si=IYPgxQBjJOLtvGod'>Efficiently Run GitHub Actions Workflows Locally with act Tool </a></li>
</ul>
