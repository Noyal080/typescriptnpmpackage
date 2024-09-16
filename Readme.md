## NPM Package Creation using Typescript and tsup
 1. mkdir add-package (suppose a package-name add-package)
 2. cd add-package
 3. npm init -y
 4. npm install react react-dom --save-dev
 5. npm install --save-dev typescript @types/react @types/react-dom tsup
 6. In your package.json inside script add or replace following lines:
 ```
		    "main": "./dist/index.js",
			"module": "./dist/index.mjs",
			"types": "./dist/index.d.ts",
			"scripts": {
				"build": "tsup"
		},
```
 7.  Create a tsconfig.json file and add the following scripts:
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
 8. Create a tsup.config.ts and add the following scripts :
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
9. Now Create a folder src and create all the necessary ***Components.tsx*** you want to work on.
10. Also add a ***index.ts*** where you import all your components:
        ```
        export { default  as  Component } from  "./Component";
		export  type { ComponentProps } from  "./Component";
        ```
11. In terminal press command ``npm run build``
12. Then ``npm login`` and use your npmjs.com login credentials
13. Use command ```npm publish --access=public``` to publish your package
 
		
