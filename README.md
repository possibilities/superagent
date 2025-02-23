<div align="center">

# Superagent 🥷

### The agent framework for large language models

<p>
<img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/homanp/Superagent" />
<img alt="GitHub Last Commit" src="https://img.shields.io/github/last-commit/homanp/Superagent" />
<img alt="" src="https://img.shields.io/github/repo-size/homanp/Superagent" />
<img alt="GitHub Issues" src="https://img.shields.io/github/issues/homanp/Superagent" />
<img alt="GitHub Pull Requests" src="https://img.shields.io/github/issues-pr/homanp/Superagent" />
<img alt="Github License" src="https://img.shields.io/badge/License-MIT-yellow.svg" />
<img alt="Discord" src="https://img.shields.io/discord/1110910277110743103?label=Discord&logo=discord&logoColor=white&style=plastic&color=d7b023)](https://discord.gg/e8j7mgjDUK" />
</p>

</div>

-----

Superagent is an open source agent framework that enables any developer to integrate production ready AI Agents into any application in a matter of minutes.

-----

## 🎥 Demo

https://github.com/homanp/superagent/assets/2464556/d02a05d0-64e6-48a2-a102-fb1312105fa5

## 🧐 Tutorials

We post tutorials regularly on our [Youtube channel](https://www.youtube.com/channel/UCBeXnF8gh2EwAmOIwpmfjmA). Make sure to check them out! 

## ✨ Use cases

Superagent allows you to build any AI application/micro service you want, including:

- Question/Answering over Documents (LLM Finetuns/Vectorstores)
- Chatbots
- Co-pilots & AI assistants
- Content generation
- Data aggregation
- Workflow automation


## 👀 Features

- Memory
- Streaming
- Custom finetuning 🆕
- Python/Typescript SDKs
- REST API
- API connectivity
- Vectorization
- Support for proprietory and OSS LLMs
- API concurrency


## 📋 Documentation
For full documentation, visit [docs.superagent.sh](https://docs.superagent.sh)

To see how to contribute, visit [Contribution guidelines](https://github.com/homanp/Superagent/blob/main/.github/CONTRIBUTING.md)

## 🛠️ Getting started

Clone the Superagent repository into a public GitHub repository or fork it from [https://github.com/homanp/superagent/fork](https://github.com/homanp/superagent/fork). 

If you plan to distribute the code, keep the source code public.

Both the API and UI require a database in order to work. We recommend settings this up on Supabase. 

<details>
<summary>Setting up Supabase</summary>

Create a [Supabase](https://supabase.com) account and project. 
We have seperated the ui and api into two sepearate Supabase projects which is recommended due the fact that the api runs on `prisma`.

**Supabase setup for Superagent UI project**

1. Run the migrations (checkout Superagent UI section for this)
    ```sh
    supabase migration up (locally)
    supabase db push (cloud)
    ```
2. Run the following query to setup authentication:
    ```sh
    -- inserts a row into public.profiles
    create function public.handle_new_user()
    returns trigger
    language plpgsql
    security definer set search_path = public
    as $$
    begin
    insert into public.profiles (user_id)
    values (new.id);
    return new;
    end;
    $$;

    -- trigger the function every time a user is created
    create trigger on_auth_user_created
    after insert on auth.users
    for each row execute procedure public.handle_new_user();
    ```

3. Create a Supabase storage

4. Set storate permissions:
   Set the following policy for `storage.objects`
   <img width="2672" alt="Screenshot 2023-09-14 at 23 27 35" src="https://github.com/homanp/superagent/assets/2464556/8d6bde18-528e-4e0a-9840-aabe39ce5e68">

    
</details>

<details>
<summary>Setting up Github OAuth in UI</summary>

1. Create a new Github OAuth app in your [Github account](https://github.com/settings/developers)

2. Copy the `CLIENT_ID` and `CLIENT_SECRET` and paste them into the `.env` variabels in the Superagent UI project.

3. Set the following callback URL
    ```sh
    <YOUR_SUPABASE_URL>/auth/v1/callback
    ```
4. Navigate to your Supabase project you have created for Superagent UI and paste the `CLIENT_ID` and `CLIENT_SECRET`

<img width="2672" alt="Screenshot 2023-09-15 at 09 08 52" src="https://github.com/homanp/superagent/assets/2464556/abd1e2fb-df90-413a-b674-766343683f6c">

**NOTE**: You can enable any provider using the steps above.
    
</details>

<details>
<summary>Superagent API</summary>

1. Navigate to `/libs/superagent`

2. Rename the `env.example` to `.env`  and make sure you have all mandatory values set

3. Create a virtual environment

    ```sh
    virtualenv venv
    source venv/bin/activate
    ```

4. Install dependencies

    ```sh
    poetry install
    ```

5. Run database migrations

    ```sh
    poetry run prisma migrate dev
    ```

6. Start the server

    ```sh
    uvicorn app.main:app --reload
    ```
</details>

<details>
<summary>Superagent UI</summary>

1. Navigate to `/libs/ui`

2. Rename the `env.example` to `.env`  and make sure you have all mandatory values set

3. Install the dependencies:

    ```sh
    npm install
    ```
4. Run migrations:
    ```sh
    supabase migrate up (local)
    supabase db push (cloud)
    ```

4. Run the development server

    ```sh
    npm run dev

    ```

</details>

<details>
<summary>Superagent legacy</summary>
    
Please refer to the [README](https://github.com/homanp/superagent/blob/v2/libs/legacy/README.md) in `/libs/legacy` for further instructions.

</details>


## 🫶 Contributions

Superagent is an open-source project, and contributions are welcome. If you would like to contribute, you can create new features, fix bugs, or improve the infrastructure. Please refer to the [CONTRIBUTING.md](https://github.com/homanp/Superagent/blob/main/.github/CONTRIBUTING.md) file in the repository for more information on how to contribute


## ⭐ Acknowledgements

We want to give a big shout out to following open source projects, without which Superagent wouldn't be possible.

- [FastAPI](https://github.com/tiangolo/fastapi)
- [Prefect](https://github.com/PrefectHQ/prefect)
- [Supabase](https://github.com/supabase/supabase)
- [next.js](https://github.com/vercel/next.js)
- [Vercel](https://github.com/vercel)
- [Fern](https://github.com/fern-api/fern)
- [Langchain](https://github.com/langchain-ai/langchain)
- [LlamaIndex](https://github.com/jerryjliu/llama_index)
- [Prisma](https://github.com/prisma/prisma)
- [Resend](https://github.com/resendlabs)
- [Motorhead](https://github.com/getmetal/motorhead)
