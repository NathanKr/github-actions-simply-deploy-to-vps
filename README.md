<h1>Project Name</h1>
....



<h2>Project Description</h2>
....

<h2>Motivation</h2>

<h3>The problem</h3>
You have a private repo on Github and you want to deploy it to VPS upon git post to main branch using a workflow file

The following technologies are used:

<ul>
 <li>SSH</li>
 <li>public \ private key authentication (VPS)</li>
 <li>Github Actions</li>
</ul>


<h2>Installation</h2>
....



<h2>Usage</h2>
....



<h2>Design</h2>
<h3>High level schema</h3>
There are four components
<ul>
<li>your local machine - issue from here e.g. git push to main branch</li>
<li>Github - your private repo to be deployed on VPS is here</li>
<li>Github Actions Runner - this run the workflow file</li>
<li>VPS - here the private repo is deployed</li>

</ul>
todo nath ---> make this an image
<img src='./figs/high-level-schema.drawio'/>

<h3>Design questions</h3>
<ul>
 <li>should i use ssh agent </li>
 </ul>

<h3>Design question : the repo is privte so how to access it</h3>
Using github actions the best solution is to use GITHUB_TOKEN . 


<h3>Design question : how the vps get the repo</h3>

<ol>
<li>clone by the vps . runner need to copy GITHUB_TOKEN to the vps</li>
<li>trnasfer from the runner to the vps using ssh .runner use GITHUB_TOKEN and scp to copy the repo to the vps</li>
</ol>


<h3>Design question : where to store VPS SSH private key so the runner can access it </h3>
The best solution to store screts in github is to use Github secrets which is part of the repo. And this is what i will use

<h2>Code Structure</h2>
....

<h2>Demo</h2>
....

<h2>Points of Interest</h2>
<ul>
    <li>...</li>
   
</ul>

<h2>References</h2>
<ul>
    <li><a href='https://www.youtube.com/watch?v=R48-UaZ4q1k'> SSH Essentials in 7.5 minutes </a></li>
</ul>

