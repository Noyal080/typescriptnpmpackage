## NPM Package Creation using Typescript, Tailwind CSS and tsup
 1. mkdir add-package (suppose a package-name add-package)
 2. cd add-package
 3. npm init -y
 4. npm install react react-dom --save-dev
 5. npm install --save-dev typescript tailwindcss postcss autoprefixer tsup @types/react @types/react-dom postcss-cli
 6. Enter the code in the terminal ```npx tailwindcss init -p``` . It should create two files tailwind.config.js and postcss.config.js, if not create manually.
 7. Add the following in postcss.config.js :- 
		 ```module.exports = { 
		 plugins: { 
			 tailwindcss: {}, // Use Tailwind CSS plugin
			 autoprefixer: {}, // Use Autoprefixer for adding vendor prefixes 
				  }, 
		  };
		 ```
		 And for tailwind.config.css
		 ```
		module.exports  = {
		content: ["./src/**/*.{js,jsx,ts,tsx}", "./index.html"],
		theme: {
		extend: {},
		},
		plugins: [],
		};```
 8. In your package.json inside script add or replace following lines:
 ```
		    "main": "dist/index.js",
			"module": "dist/index.mjs",
			"types": "dist/index.d.ts",
			"scripts": {
				"build": "tsup src/index.ts --format cjs,esm --dts && npm run build:css",
				"build:css": "postcss src/styles/global.css -o dist/tailwind.css"
			},
```
 9.  Create a tsconfig.json file and add the following scripts:
```
	    {
	    "compilerOptions": {
		"target": "ES2022",
		"module": "ESNext",
		"jsx": "react-jsx", // Use "react-jsx" for React 17+
		"moduleResolution": "node",
		"esModuleInterop": true,
		"skipLibCheck": true,
		"strict": true,
		"forceConsistentCasingInFileNames": true,
		"declaration": true,
		"declarationDir": "dist",
		"outDir": "dist"
},
"include": ["src/**/*"]
}
```
 10. Create a tsup.config.ts and add the following scripts :
 ``` 
	import { defineConfig } from  "tsup";
	export  default  defineConfig({
	format: ["cjs", "esm"],
	entry: ["./src/index.ts"],
	sourcemap:  true,
	dts:  true,
	shims:  true,
	skipNodeModulesBundle:  true,
	clean:  true,
	external: ["react", "react-dom"],
});
 ```
11. Now Create a folder src and create all the necessary ***Components.tsx*** you want to work on.
12. In the src folder create a style folder and a file tailwind.css where you write the following:
		```
		@tailwind base;
		@tailwind components;
		@tailwind utilities;
		```
		
13. Also add a ***index.ts*** where you import all your components:
        ```
        import './styles/tailwind.css';
        export { default  as  Component } from  "./Component";
		export  type { ComponentProps } from  "./Component";
        ```
14. In terminal press command ``npm run dev``
15. Then ``npm login`` and use your npmjs.com login credentials
16. Use command ```npm publish --access=public``` to publish your package

To use this package
1. Install the package
2. Then import the necessary Component
3. In Index.js import the following
	import "packagename/dist/index.css";
 
		
