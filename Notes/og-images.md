---
original_path: Notes/Tech Learning/Misc/Next JS/og-images.md
base: TechLearning
path_area: Misc
categories:
  - "[[TechLearning]]"
  - "[[Misc]]"
---


og-images are used to generate clean previews when links are shared through social media and are implemented in the `head` component in the `html` documents. But in [[NextJs]], there are multiple ways to implement this.

### opengraph.{img,png,tsx,jsx}
A dedicated image or component at a certain route level can be used as an open-graph image for that route. The og-image is not automatically linked to the route but it can be linked in the metadata object of the page as follows. 

#### Generation

```tsx title:"app/some-page-route/opengraph-image.tsx" 

import { ImageResponse } from 'next/og'
import { readFile } from 'node:fs/promises'
import { join } from 'node:path'
 
// Image metadata
export const alt = 'About Acme'
export const size = {
  width: 1200,
  height: 630,
}
 
export const contentType = 'image/png'
 
// Image generation
export default async function Image() {
  // Font loading, process.cwd() is Next.js project directory
  const interSemiBold = await readFile(
    join(process.cwd(), 'assets/Inter-SemiBold.ttf')
  )
 
  return new ImageResponse(
    (
      // ImageResponse JSX element
      <div
        style={{
          fontSize: 128,
          background: 'white',
          width: '100%',
          height: '100%',
          display: 'flex',
          alignItems: 'center',
          justifyContent: 'center',
        }}
      >
        About Acme
      </div>
    ),
    // ImageResponse options
    {
      // For convenience, we can re-use the exported opengraph-image
      // size config to also set the ImageResponse's width and height.
      ...size,
      fonts: [
        {
          name: 'Inter',
          data: interSemiBold,
          style: 'normal',
          weight: 400,
        },
      ],
    }
  )
}



```

For a dynamic page the component automatically receives the slug as the param. i.e.

```tsx title:"app/some-page-route/opengraph-image.tsx" 

import { ImageResponse } from 'next/og'
import { readFile } from 'node:fs/promises'
import { join } from 'node:path'
 
// Image metadata
export const alt = 'About Acme'
export const size = {
  width: 1200,
  height: 630,
}
 
export const contentType = 'image/png'
 
// Image generation
export default async function Image() {
  // Font loading, process.cwd() is Next.js project directory
  const interSemiBold = await readFile(
    join(process.cwd(), 'assets/Inter-SemiBold.ttf')
  )
 
  return new ImageResponse(
    (
      // Rest of the code
	)
}

```

#### Linking
To link the image to the route, we just have to add the route where `opengraph-image` component is present.

So, for static and dynamic routes, the examples are as follows.

```tsx title="app/blog/page.tsx"

// Static Data - using metadata object
export const metadata: Metadata = {
	title: metadataInfo.title,
	openGraph: {
		type: 'website',
		url: metadataInfo.url,
		siteName: metadataInfo.siteName,
		title: metadataInfo.title,
		description: metadataInfo.description,
		images: [
			{
				url: '/blog/opengraph-image', // yourdomain/blog/opengraph-image
				width: 1200,
				height: 630,
				alt: 'aiquery.io Blog'
			}
		]
	},
	description: metadataInfo.description
};
```

```tsx title="app/blog/[slug]/page.tsx"

// Dynamic Data - using generateMetadata


export async function generateMetadata({ params }: BlogPostPageProps): Promise<Metadata> {

	// getPostBySlug is a custom function to get the data from the content source
    const post = await getPostBySlug(params.slug).catch(() => null);
  

    return {
        title: post.title,
        description: post.description,
        openGraph: {
            title: post.title,
            description: post.description,
            url: `/blog/${post.slug}`,
            images: [
                {
                    url: `/blog/${post.slug}/opengraph-image`,
                    alt: post.title
                }
                // ? Other images can be used as fallback
            ],
            // Or we can also directly use the url from a cdn like this:
            // images: post.coverImage ? [post.coverImage] : undefined
        }

    };

}
```
#### Tips/Pitfalls
- To use tailwind `tw` prop must be used instead of `className`.
- For a div enclosing an `img` tag, the `display:flex` property is crucial. Otherwise the image generation will fail.
- At any moment, the og-image can be verified by visiting the page url + `/opengraph-image`.
- Locally or remotely hosted-image can also be used directly though url/paths instead of generating the images.

## References
[Next JS Docs](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image#generate-images-using-code-js-ts-tsx)
[Youtube Shorts - Dynamic OG Generation](https://www.youtube.com/shorts/iBv8qGGSqH4)
[Youtube Tutorial - Complete OG Image Gen Guide (Static Only)](https://www.youtube.com/watch?v=QHi4XZ8K72A&pp=ygUgZ2VuZXJhdGUgb3BlbmdyYXBoIGltYWdlIGR5bmFtaWM%3D)