## NPM Package Creation using Typescript, Tailwind CSS and tsup
 1. mkdir add-package (suppose a package-name add-package)
 2. cd add-package
 3. npm init -y
 4. npm install react react-dom --save-dev
 5. npm install --save-dev typescript @types/react @types/react-dom tsup tailwindcss postcss autoprefixer

		
tsconfig.json
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
tsup.config.js
import { defineConfig } from 'tsup';

export default defineConfig({
    format: ['cjs', 'esm'],
   	 entry: ['./src/index.ts'],
     sourcemap:true,
   	 dts:  true,
   	 shims:  true,
   	 skipNodeModulesBundle:  true,
   	 clean:  true,
    external: ['react', 'react-dom'], 
}); 
