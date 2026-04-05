---
original_path: Notes/Tech Learning/Misc/Next JS/public vs assets directory.md
base: TechLearning
path_area: Misc
categories:
- '[[TechLearning]]'
tags:
- misc
---

## `Public` Folder

- Files are served statically at the root URL path (/)
- Best for:
	- Static files (images, fonts, robots.txt)
	- Files needing direct URL access
	- OpenGraph/Twitter card images
	- Files are served as-is without processing
- Usage Example (Good for metadata): 

```tsx title:"app/page.tsx"

// In metadata
  
export const metadata: Metadata = {

    title: 'aiquery.io',
    description: 'aiquery.io is a platform that simplifies security investigations and monitoring.',
    openGraph: {
        type: 'website',
        url: 'https://aiquery.io',
    },

    twitter: {
        card: 'summary_large_image',
        site: '@aiquery',
        title: 'aiquery.io - Actionable Security and IT insights at your fingertips',
        description:
            'aiquery.io is a platform that simplifies security investigations and monitoring by automating many of the tasks involved in querying and analyzing data. It helps security professionals save time, streamline workflows, and maintain better control over their environments, leading to improved overall security posture.',
        images: ['/logo-vector.png']
    }

};


```


## `Assets` Folder

- Files are processed by Next.js's build system
- Best for:
	- Images needing optimization
	- CSS/SCSS files
	- JavaScript modules
	- Components and source code
	- Gets processed, optimized, and bundled during build
- Usage Example (Good for components): 

```tsx title:"app/page/flow-section.tsx"

import HowItWorks from '@/assets/how-it-works-01.svg'
import Image from 'next/image'

const SomeComponent = ()=>{
	return <Image src={HowItWorks} alt="How it works" />
}

```

## When to Use Which?

- Use public when you need direct URL access (metadata, external services)
- Use assets when the file is part of your application's source code and needs processing

