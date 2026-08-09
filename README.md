# svelte-binder
Binderized svelte development playground.


[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/svelte-binder/HEAD)

-------------------

### How to use

Once the session launches...

1. Start a terminal and run the following command there.

	```shell
	npm create vite@latest my-firstglance-app -- --template svelte
	```

	To the two questions answer `Yes` first and then `No`.

2. Next run the following series of commands in that terminal:

	```shell
	cd my-firstglance-app 
	npm install
	```

3. Wait for the install to complete and then run the following command in that terminal to fix the config to tell Vite to allow all proxy hosts directly so jupyter-server-proxy will work:

	```shell
	sed -i 's/plugins: \[svelte()\]/plugins: [svelte()], server: { allowedHosts: true }/' vite.config.js
	npm run dev -- --host --base=${JUPYTERHUB_SERVICE_PREFIX}proxy/absolute/5173/
	```

4. Do some initial preparation in order to be ready to try things soo to look at the result of vite / svelte in your browser. Copy the URL from your browser's address bar. It will look something like `https://hub.gesis.mybinder.org/user/fomightez-svelte-binder-5uzrk280/lab`. Paste it in a text editor so that you can get the part in front of `lab` for later.

5. Run the following command in that terminal where you ran the earlier commands to start the development server serving the content:

	```shell
	npm run dev -- --host --base=${JUPYTERHUB_SERVICE_PREFIX}proxy/absolute/5173/
	```

6. Now you want to view what is being served. In your text editor, edit the collected URL to replace the `lab` part with `proxy/absolute/5173/`. So your edited URL should look something like this:

	```text
	https://hub.gesis.mybinder.org/user/fomightez-svelte-binder-5uzrk280/proxy/absolute/5173/
	```

Open a new browser window and paste in your edited URL so you can look at the site being served.

