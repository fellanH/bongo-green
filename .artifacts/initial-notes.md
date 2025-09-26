#Initial Notes

I'm building an application that interfaces with the fal.ai api and has a shadcn dashboard interface where I can run pre-configured workflows, see generated assets, select generated assets for use in other workflows, the assets are generated on the FAL.ai servers and provide a handy public url that can be used to trigger workflows, I want to build this up step by step and not make any huge changes at first, focus on planning this all out correctly and work away at adding features as I go along, the long term goal of this project is however to launch a fully build web application that I can let users on to.

Fal has a workflow feature that I like and that we can use through the api to get started quickly, later I want to replicate this feature in my own app, this is the core of the idea

LLM Workflow API - Fal.ai
LLM API providers - Fal.ai, wavespeed.ai, ChatGPT, Gemini, Claude, etc.
Hosted LORA provider - HuggingFace, LORA files can also be self hosted in the application we can explore this further.

Requirements:

The no code visual interface should be very similar to how figma works, I think they have nailed the UX for a digital workspace, The user should be able to add models and generate outputs via api calls to different hosted LLMs, initally I want to focus on FAL.AI FLUX DEV text-to-image with LORA support and WAN2.2 Image-to-video with custom LORAs, But I could see connecting with Gemini API and ChatGPT aswell for text based generation, similar to what we are doing now but in a figma like UI.

Asset management is Key in this project, I need a scaleable solution with low inital configuration, I have my eyes on supabase and have some experience in it so starting there would be ideal, I want to be able to offer both persistant and non persistant storage, FAL.ai provides hosted URLs of generated assets for a week or two after generation, we can utilize this feature to keep costs low initially.

For payments i'm exploring polar.sh a promising payment startup focused on AI SaaS, I also have stripe already so we can use that aswell, but please advise on what to use here.

for the MVP we need Admin, Free user, Pro User, The admin role needs to be highly protected and maybe even IP locked to only my computer even for the mvp. There could be catastrophic billing issues if the security got breached even in the mvp stage since these api calls are so expensive.

Inital performance can be avrage, as long as the front-end is snappy and responsive we can use skeleton loaders to wait for server-side code and api calls. Later we can improve the api call speed etc but for now just standard FAL.ai waittimes are fine.

Security is of the utmost importance in this project since it will contain sensitive data and expensive api calls. we need to take great care at this stage.

MVP is a few tens of users maybe 50 max but the first launch might see a few thousand users, if all goes to plan seeing way more than that should be possible to achive without too much of a headache later down the line.



Let me know if you need any additional information


# What is the primary problem this application solves for users?

Using existing interfaces for more complex AI generated content is limited, too technical / hard to use or just doesn't exist yet. I want to utilize the strength of existing solutions on the market and stich them toghether to create a highly custom product based on my own needs. the product should evolve with me and be a playground for testing new ideas, I also want to monetize it as soon as possible to start generating income to be able to push innovation faster. My initial idea was to use FAL.ai and their existing vast library of well functioning t2i and i2v models. Later on I might add other distributors or fully host my own models on google cloud compute or my own servers.

# User persona 

A software engineer, product manager, or startup founder working on an application that needs to integrate generative AI, but they are not a machine learning expert.

I like this persona the most the reason being they have more impact, bigger problems that we can solve, and they are quicker to reach for their wallet. We could include other models and frameworks and allow the user to add custom models easlily themselves. I'm also thinking we can branch out to other AI usecases like AI-Chat with pre-programmed promts etc. Sky's the limit here, we just need to start bootstrapped and low complexity and build a framework that scales automatically as the userbase grows, inbuilt customization in a smart way should be able to solve this.

# Monetization 

Usage-based pricing (pay-as-you-go).
Core functionality is free or have a minimal subscription fee. Users pay per "job" or per "credit" consumed by the underlying Fal.ai API calls.

# Project Goals (MVP)

allow users to quickly select from a predefined library of generative AI models (starting with fal.ai's t2i and i2v models). Enable the user to chain together these models in a simple, no-code visual interface. Provide a centralized location to view and manage all generated assets, including their public URLs.


