## NPM Package Creation using Typescript, Tailwind CSS and tsup
 1. mkdir add-package (suppose a package-name add-package)
 2. cd add-package
 3. npm init -y
 4. npm install react react-dom --save-dev
 5. npm install --save-dev typescript @types/react @types/react-dom tsup tailwindcss postcss autoprefixer
 6. Enter the code in the terminal ```npx tailwindcss init -p``` . It should create two files tailwind.config.js and postcss.config.js, if not create manually.
 7. If postcss.config.js isnot created manually add the following :- 
		 ```module.exports = { 
		 plugins: { 
			 tailwindcss: {}, // Use Tailwind CSS plugin
			 autoprefixer: {}, // Use Autoprefixer for adding vendor prefixes 
				  }, 
		  };
		 ```
 8. In your package.json inside script add or replace following lines:
 ```
		    "main": "./dist/index.js",
			"module": "./dist/index.mjs",
			"types": "./dist/index.d.ts",
			"files": [ "dist", "src/styles" ],
			 "scripts": { 
					"build": "tsup", // Builds the package using Tsup
					"build:css": "postcss src/styles/tailwind.css -o dist/tailwind.css", 
					 "dev": "npm run build:css && npm run build --watch", 
					 }
```
 9.  Create a tsconfig.json file and add the following scripts:
```
	    {
		"compilerOptions": {
			"strict": true,
			"noImplicitAny": true,
			"esModuleInterop": true,
			"strictNullChecks": true,
			"target": "ES2022",
			"moduleResolution": "Node10",
			"module": "CommonJS",
			"declaration": true,
			"isolatedModules": true,
			"noEmit": true,
			"outDir": "dist",
			"jsx": "react-jsx",
		},
		"include": ["src"],
		"exclude": ["node_modules", "dist", "**/__tests__/*"]
	}
```
 10. Create a tsup.config.ts and add the following scripts :
 ``` 
	 import { defineConfig } from  'tsup';
	 export  default  defineConfig({
		 format: ['cjs', 'esm'],
		 entry: ['./src/index.ts'],
		 dts:  true,
		 shims:  true,
		 skipNodeModulesBundle:  true,
		 clean:  true,
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
 
		
