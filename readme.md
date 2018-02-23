
# Offline First Project Manager
An offline-capable project management tool, built as a Progressive Web App by [Teri Chadbourne](https://github.com/terichadbourne).

For more on how this Progressive Web App (PWA) was built using PouchDB, CouchDB, Service Worker, and a Wep App Manifest, stay tuned for an upcoming beginner-friendly blog series. 

## The purpose of the app

### For me, as a project management tool:
This app is an offline-capable project management tool that I built to track the status of blog posts in the works for the [Offline Camp Medium publication](http://medium.com/offline-camp). Using a simple web form, which uses logic to hide and reveal certain questions depending on the data entered, it stores a record for each article in progress and lets me come back and edit that record later. It also creates a second webpage I can share with an author to provide resources they need and request resources I need in return. 

Because I need to start this process while I'm on site at [Offline Camp](http://offlinefirst.org/camp) with very limited internet access, the app needs to load while offline and allow me to edit and save data without an internet connection. Since I collaborate with other editors and own many gadgets, the data ultimately needs to sync across multiple devices, browsers, and users. It requires an [Offline First](http://offlinefirst.org) design.  

### For you, as a sample implementation of an offline-capable Progressive Web App:
You can explore my code to see how PouchDB, Apache CouchDB™, Service Worker, and a Web App Manifest are used to create an Offline First experience in the form of a Progressive Web App. The nuances of what I'm using my own web form for don't matter. In fact, you'd most likely want to clone the repo and adapt the form logic to create another offline-capable, form-based web app that meets the custom needs of your own project.

This is a simple, beginner-friendly web application built using only client-side code. In addition to its custom JavaScript, HTML, and CSS files, it relies on the great sync powers of PouchDB library. jQuery.js and normalize.css are used out of convience to simplify the front-end development, while Node.js and Express are used only to serve the project up locally for review. You don't need to understand server-side development to see what makes this application tick.


## The Offline First functionality

The [Offline First](http://offlinefirst.org) approach to web development plans for the most constrained network environment first, enabling a great user experience even while the device is offline or has only an intermittent connection, and providing progressive enhancement as network conditions improve. This design also makes apps incredibly performant (fast!) on the best of networks. 

PouchDB, CouchDB, Service Worker, and a Wep App Manifest are the primary tools that turn this simple project management tool into a high-performance, offline-capable Progressive Web App.

**Data stays safe on your device, even while it's offline.**  
Persistance of data entered by the user is achieved using the in-browser database PouchDB. This will allow your data to survive between sessions and when disconnected from the network. (Whether you're offline at an event or back in the office on your trusty Wi-Fi, you can still add new projects and modify existing ones.)

**Data syncs between devices when a connection is available.**  
When a connection is available, the data is synced from the local device to a CouchDB database in the cloud, and can thus be shared across multiple devices or users. (Managing a project with a partner or need to access the data on both your phone and your laptop? No problem!)

**The app loads quickly, even while offline.**  
To keep the app itself functional while offline, a Service Worker is used to cache page resources (the most important HTML, CSS, and JavaScript files) when the web application is first visited. Each device must have a connection for this first visit, after which the app will be fully functional even while offline or in shoddy network conditions. (No more error messages or frustratingly slow page loads.)

**The app can be installed on a mobile device.**  
In combination with the Service Worker used for caching, a Web App Manifest containing metadata allows the app to become a Progressive Web App, an enhanced website that can be installed on a mobile device and can then be used with or without an internet connection. (It's secretly still a website, but you can access it through one of those handy dandy little app icons on your homescreen!)

Explore the code in this GitHub repository to see how the Offline First design is applied.


## Running the App

To see the Offline First functionality in action, you'll need to follow the steps below. 

**A note on security:** To keep the focus on the front-end code that provides the app's offline functionality, this sample implementation has simplified the server-side elements and **does not currently protect your login credentials** for CouchDB. It is not suitable for production**. (See the **[security note](#important-security-note)** below for more detail.)

### Quick instructions for experienced coders:
_(The **TL;DR** you're looking for if you're already familiar with the command line, Node.js, NPM, Git, GitHub, and CouchDB.)_
1. Clone the repo and run `npm install`.
2. Set up a new remote CouchDB database with CORS enabled.
3. Add a new file titled `credentials.js` to the `js` directory. The one line of code in this file should be: 

        var remoteCouch = "YOUR_REMOTE_COUCHDB_URL_HERE";

4. Run `npm start` from the project directory and go to http://localhost:8000/.
5. Due to [security concerns](#important-security-note), don't let anyone else use the app while you're running it.

### Detailed instructions:

#### 1. Get set up with Node, NPM, Git, and GitHub:
- Install Node and NPM. (Check out these installation tutorials for [Mac](http://blog.teamtreehouse.com/install-node-js-npm-mac) or [Windows](http://blog.teamtreehouse.com/install-node-js-npm-windows) if needed.)
- [Set up Git and GitHub](https://help.github.com/articles/set-up-git/).

### 2. Clone the repo and install dependencies:
- From the command line, navigate to the directory (folder) inside of which you'd like to store this project. (Here's a [command line tutorial](https://tutorial.djangogirls.org/en/intro_to_command_line/) if you need it.)
- Clone this repo by typing: 
```
git clone https://github.com/ibm-watson-data-lab/offline-first-project-manager.git
```
- Navigate into the project directory (the folder containing the cloned repo) by typing `cd offline-first-project-manager`.
- Type `npm install` to install this project's dependencies. This will set you up with the files you need for Express, a Node.js web application framework that will deal with some server stuff while we focus on the client-side code.

### 3. Create a CouchDB database and API key and enable CORS:
- Create an empty CouchDB database and get yourself set up with an API key. 
- If you haven't used CouchDB before, one easy option is to create a new database on Cloudant, which takes care of the hosting for you. After creating a new database, click on Permissions and then Generate API Key. Write down the Key and Password generated in a safe place, because Cloudant will never show them to you again. 
- You'll need a URL that references your database, with your top-secret API key built in. If you choose to use Cloudant, it will look like this: 

        https://KEY:PASSWORD@USERNAME.cloudant.com/<DATABASE>
- Ensure Cross-Origin Resource Sharing (CORS) is enabled on your database. (If using Cloudant, visit the CORS tab in your user settings.)

### 4. Create a credentials file (SEE SECURITY NOTE BELOW)
- Navigate into the `js` directory by typing `cd js`. 
- Create a new JavaScript file in this directory titled `credentials.js`. It's very important that you spell this correctly, since the filename is already referenced in your `.gitignore` file to prevent accidental upload of your CouchDB credentials to GitHub at a later date. 
- Add the following line of code to your `credentials.js` file, inserting the URL you establish in Step 1 and keeping the quotation marks you see here: 

        var remoteCouch = "YOUR_REMOTE_COUCHDB_URL_HERE";

- Save the file and exit your editor.

### 5. Launch the app (SEE SECURITY NOTE BELOW):
- Navigate back to the main project file using `cd ..`.
- Type `npm start` and wait until you see the message `server is listening on 8000`
- To load the app, open a modern Chrome or Firefox browser (to ensure you receive all the benefits of Service Worker) and navigate to: http://localhost:8000/
- To stop the server when you're done (or for testing purposes as described below, use Control-C.

### IMPORTANT SECURITY NOTE: 
Although your `credentials.js` file won't be tracked by Git or uploaded to GitHub, it is among the files that will be served up when you launch the app. This means that a user could therefore inspect your code and view the contents of the file, gaining access to your remote database. **This setup is not suitable for production.**

For an example of a PWA built using the same technologies with more robust security measures, check out this [sample implementation of a shopping list app](https://github.com/ibm-watson-data-lab/shopping-list-vanillajs-pouchdb). It requires each user, device, or browser to enter their own CouchDB credentials, which are stored locally in PouchDB.



## Testing the Offline First functionality

### Test offline data entry and syncing between devices (PouchDB & CouchDB): 
A new PouchDB database will be created in each browser you use to test the app. A great way to explore the offline syncing powers of PouchDB and CouchDB
is to load the site in both Chrome and Firefox (modern implementations of which support service workers), thinking of them each as a different user or device. 

You can now explore what happens if one user is online and another isn't. To do this, set just one browser to offline mode. (In Chrome, open the developer tools and select Network or Applications and then check the Offline box. In Firefox, go to Web Developer, then check Work Offline. In either case, you must refresh the page for the effect to take the place.) 

Because the app files are hosted locally, this process will only simulate disconnecting from the remote CouchDB database, not from the resources that make up the page itself (the HTML, CSS, and JS files that create the user experience).

### Testing caching of resources (Service Worker): 
In order to simulate loading the page from scratch while you're offline (after at least once accessing it while online), you'll need to kill the local server you started (by typing `Ctrl-C` in Terminal) and refresh the page. The
service worker should have cached relevant resources so you should see no change in functionality with this test. (On a website without a Service Worker, you'd be seeing a 404(?) error or Chrome's famous downasaur.)

### Testing installing to homescreen (Web App Manifest): 
Something with Ngrok TBD


## Resources and additional reading 
- Blog series coming soon!
- [PouchDB](https://pouchdb.com/) 
- [Apache CouchDB™](http://couchdb.apache.org/)
- [IBM Cloudant](https://www.ibm.com/cloud/cloudant)
- [Service Worker](https://developers.google.com/web/fundamentals/primers/service-workers/)
- [Web App Manifest](https://developers.google.com/web/fundamentals/web-app-manifest/)
- [Progressive Web Apps](https://developers.google.com/web/progressive-web-apps/)
- [Offline First](http://offlinefirst.org/)
- [Offline Camp](http://offlinefirst.org/camp/)
- [Offline Camp Medium publication](https://medium.com/offline-camp)
- [Additional Offline First resources](https://medium.com/offline-camp/offline-first-resources-2acc5836e9d4)
- [Offline First sample implementations in a variety of stacks](https://ibm-watson-data-lab.github.io/shopping-list/)

## License
[Apache 2.0](LICENSE)
