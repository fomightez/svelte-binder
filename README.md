# svelte-binder
Binderized svelte development playground.


[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/fomightez/svelte-binder/HEAD)

-------------------

### How to use

Pick a track. (**You most likely want track B with SvelteKit!**)

Track A: Vanilla Vite + Svelte Playground
Best for: Learning Svelte template syntax, state management (`$state`), and building single-page components.

Track B: SvelteKit DEvelopment Playground 
Best for: Leanring All-round modern, Svelte, learning filesystem routing, layouts, and page-to-page navigation.

StackBlitz or CodeSandbox may be better options, if you don't mind signing up.

Next, click the '`launch binder`' badge above to start a MyBinder-served Jupyter session.   



Once the session launches, do the steps for whichever track you chose...

## Track 2: SvelteKit Development Playground (Standard Approach)

1. Start a terminal and run the following command there.

	```shell
	npm create vite@latest my-firstglance-app -- --template svelte
	```

	To the two questions, answer `Yes` to the first and then `No`.

2. Next run the following series of commands in that terminal:

	```shell
	cd my-firstglance-app 
	npm install
	```

3. Wait for the install to complete and then run the following command in that terminal to fix the config to tell Vite to allow all proxy hosts directly so jupyter-server-proxy will work:

	```shell
	sed -i 's/plugins: \[svelte()\]/plugins: [svelte()], server: { allowedHosts: true }/' vite.config.js
	```

4. Do some initial preparation in order to be ready to try things soon to look at the result of vite / svelte in your browser. Copy the URL from your browser's address bar. It will look something like `https://hub.gesis.mybinder.org/user/fomightez-svelte-binder-5uzrk280/lab`. Paste it in a text editor so that you can get the part in front of `lab` for later.

5. Run the following command in that terminal where you ran the earlier commands to start the development server serving the content:

	```shell
	npm run dev -- --host --base=${JUPYTERHUB_SERVICE_PREFIX}proxy/absolute/5173/
	```

6. Now you want to view what is being served. In your text editor, edit the collected URL to replace the `lab` part with `proxy/absolute/5173/`. So your edited URL should look something like this:

	```text
	https://hub.gesis.mybinder.org/user/fomightez-svelte-binder-5uzrk280/proxy/absolute/5173/
	```

	Open a new browser window and paste in your edited URL so that you can look at the site being served. (You may need to wait approximately a minute after running the `npm run dev` command. You can keep reloading your browser page to try.)   
	Revel in your resulting site!


## Track 2: SvelteKit Development Playground (Standard Approach)

Use this method if you want to explore SvelteKit, which is the official framework for building full Svelte websites with automatic folder-based routing. This path initializes a fully styled, multi-page demo application complete with animations and layout routing out of the box.

Once your MyBinder session launches, open a terminal and run the following steps:

1. Create the SvelteKit application structure:
   ```bash
   npx sv create my-sveltekit-app
   ```
   *Interactive Prompt Guide:*
   * **Which template?** Select **SvelteKit demo app** using your arrow keys and press Enter. *(Note: If you prefer a completely blank canvas instead, you can choose "SvelteKit minimal" here).*
   * **Add options?** Select **No** to type checking, scroll to **Done**, and press Enter.
   * **Add packages?** Scroll straight down to **Done** and press Enter.
   * **Which package manager?** Select **npm** to automatically install dependencies.

2. Move into your newly created project directory:
   ```bash
   cd my-sveltekit-app
   ```

3. Create the Vite bundler configuration to allow the MyBinder connection:
   ```bash
   cat << 'EOF' > vite.config.js
   import { sveltekit } from '@sveltejs/kit/vite';
   import { defineConfig } from 'vite';

   export default defineConfig({
       plugins: [sveltekit()],
       server: {
           allowedHosts: true
       }
   });
   EOF
   ```

4. Create the SvelteKit configuration file to correctly set up base path routing:
   ```bash
   cat << 'EOF' > svelte.config.js
   /** @type {import('@sveltejs/kit').Config} */
   const config = {
       kit: {
           paths: {
               base: process.env.JUPYTERHUB_SERVICE_PREFIX ? process.env.JUPYTERHUB_SERVICE_PREFIX + 'proxy/absolute/5173' : ''
           }
       }
   };

   export default config;
   EOF
   ```

5. Prepare your preview URL. Copy the URL from your browser's address bar. It will look something like this:
   `https://mybinder.org`
   
   Paste it in a text editor and replace the `/lab` part at the end with `/proxy/absolute/5173/`. Keep this modified URL ready.

6. Start the development server:
   ```bash
   npm run dev -- --host
   ```

7. Open a new browser window or tab, paste your modified URL, and hit Enter. Give it about a minute to spin up, and reload if necessary to see your live SvelteKit app!

*Tip: If you ever want to switch back and test display a minimal, raw setup, you can re-run these steps from the beginning using a different folder name in Step 1 (e.g., `npx sv create my-minimal-app`) and choosing the **SvelteKit minimal** option. The config files in Steps 3 and 4 remain identical.*

