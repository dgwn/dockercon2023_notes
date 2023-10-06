# DockerCon 2023

## Table of Contents

- Pre-Conference Workshop

  - [Getting Started with Docker](#getting-started-with-docker)
  - [Docker for Web Development](#docker-for-web-development)
  - [Other Sessions](#other-sessions)

- Day 1
  - [Keynote 1: Accelerating Secure App Development](#keynote-1-accelerating-secure-app-development)
    - [Docker Scout](#docker-scout)
    - [Next-Gen Build](#next-gen-build)
    - [Docker Desktop](#docker-desktop)
  - [Container Images: Interactive Deep Dive](#container-images-interactive-deep-dive)
  - [Fast, Cheap, and Portable: How Docker Made UI Testing Accessible for Everyone](#fast-cheap-and-portable-how-docker-made-ui-testing-accessible-for-everyone)
  - [15 Tips and Tricks to Improve Your Compose Experience](#15-tips-and-tricks-to-improve-your-compose-experience)
  - [New Developments in Compose](#new-developments-in-compose)
  - [Streamlining CI/CD with Modern Container Builds](#streamlining-cicd-with-modern-container-builds)
- Day 2
  - [Keynote 2: Docker & AI](#keynote-2-docker--ai)
  - [Getting Started with Wasm, Docker, and Kubernetes](#getting-started-with-wasm-docker-and-kubernetes)
  - [Things You Always Wanted to Know About Building Platforms](#things-you-always-wanted-to-know-about-building-platforms)
  - [AI Anytime, Anywhere: Getting started with LLMs on your Laptop Now!](#ai-anytime-anywhere-getting-started-with-llms-on-your-laptop-now)
  - [Debugging Innovation](#debugging-innovation)

Note: This is a personal summary of the sessions I attended at DockerCon 2023. It is not an official summary and may contain errors or omissions. I have included links to the official videos, workshop repositories, or slides where available. Some video links may be private and restricted to attendees but Docker typically makes them available to the public after a few weeks. Check their [YouTube channel](https://www.youtube.com/@DockerIo) to see if they've been added.

## Pre-Conference Workshop

### Getting Started with Docker

- [Video](https://www.dockercon.com/2023/v/s-1619667?i=ATGAD_D00OSfzT00F1xK1mBamleQecH_)
- [Workshop Repo](https://github.com/mikesir87/dockercon23-workshop-materials)

### Docker for Web Development

- [Video](https://www.dockercon.com/2023/v/s-1619671?i=ATGAD_D00OSfzT00F1xK1mBamleQecH_)
- [Workshop Repo](https://github.com/tippexs/dockercon23-webdev)

### Other Sessions

- [Links](https://www.dockercon.com/2023/preconondemand?i=ATGAD_D00OSfzT00F1xK1mBamleQecH_)

## Day 1

### Keynote 1: Accelerating Secure App Development

- Docker had been open-source for 10 years
- Web Assembly support launched in the last year
- Docker Init launched
  - auto generates a boilerplate configuration
- Cruise Automobiles gives a demo of their workspace
- Supported LLM growth, Open science intiatives, and mobile/IoT tools
- Goal is to reduce toil, improve quality of life for developers
  - Reduce friction when adopting new patterns:
    - Technologists are creatives; enable autonomy for developers to manage risk, communciate trust and give pride of ownership
    - Invite developers into knowledge communities (e.g. Open Source) to help them adapt their skills to other realms
    - Figure out how to bring devs closer to their clients for better communication
- New partnership between Docker and Udemy
  - new Docker accredited content vetted by instructional designers
  - all curricula will be publicly available for content creators
  - There are also a number of learning resources and tutorials available within Docker Desktop 'Learning Center'
- Focus today is on Cloud, tomorrow on AI.

- #### Docker Scout
  - Challenges that need to be addressed:
    - Builds can take too long on local laptop environments and debugging can be too complex
    - Software supply chain issues can cause time sinks
    - Images can be a black box
  - Image Analysis and Guided Remediation
    - checks for vulnerabilities
  - Policy Evaluation
    - analyze whether you're using best practices based on incremental positive change
    - codify quality standards
      - e.g. a policy to keep base image up-to date
  - Integrations
    - Integrates with with source code(Github, Gitlab), CI (Github Actions), code quality
  - CLI tool
  - Shows CVEs (vulnuerabilities) and how to fix them
- #### Next-Gen Build
  - Builds sometimes can take too long and tax local machines
  - Next Gen Build can be 8x+ faster
    - build moved off machine into cloud and then pushed back to local machine
    - shared cache among team
    - never need to build twice
  - Docker Desktop can show your build, cloud builds, team builds all together
- #### Docker Desktop
  - completing integration of mutagen into Docker Desktop
    - mutagen is a file synchronization tool
    - up to 17x faster
  - Docker Debug
    - available in Extension marketplace
      - debugging happens in container/shell not extension
    - Debugging for difficult situations like when container hasn't even started (or crashed)
    - bring all of the tools you need into the container
    - Old Exec (console) tab can be crude
      - no autocomplete, no nano, emacs, htop, ping, etc.
    - Access via extension allows use of buil-in tools like the above from the command line without having to "actually" install the tools, which can be a security risk or cause clutter

### Container Images: Interactive Deep Dive

The presenter's screen (with slidedeck and dev environment) wasn't shared with virtual attendees for the first 15 minutes of this session, so it was hard to follow along. Here's what I was able to get:

- Image index is composed of a JSON structure of layers and config, manifests
- Why push to a registry?
  - Deduplication
  - Metadata (tags)
  - Versions
- Pulling an image
  - 1. Convert tag to digest
    - HEAD request on manifest layers
  - 2. Select the image for the right platform
  - 3. Download config and layer blobs
  - 4. Combine layers and run image
- Beyond Images
  - Store things other than container images
    - you can publish a docker compose file as OCI image manifest
    - Homebrew as OCI image manifest
    - Helm charts...
    - Wasm modules...
    - Docker Volumes...
  - Extend container images with related, non-runnable data
    - Inline documentation
    - Runbooks
  - OCI Image and Distrivutiuon Specs v1.1
    - How to create and store alternative artifacts
    - Manifest file for establishing relationships
    - Query relationships
    - https://opencontainers.org/posts/blog/2023-07-07-summary-of-upcoming-changes-in-oci-image-and-distribution-specs-v-1-1

### Fast, Cheap, and Portable: How Docker Made UI Testing Accessible for Everyone

- UI testing with Docker Selenium
- previous alternatives:
  - VMs
    - browsers and runtimes installed
    - keep them running
    - not adequate for task
  - Headless
    - PhanotmJS, HTML Unit
    - Not real browsers
  - Reomte Execution
    - shared infrastructure
    - bottlenecks
    - network config needed
- UI testing challenges
  - context shifting is disruptive
  - complex setup
  - high costs
    - slow onboarding
    - unusable laptops while tests run
- Docker Selenium
  - enable developers to execute browser automation simply and remotely
  - run code locally and direct commands to a remote instance
  - similar to VNC viewers
  - one way: you can start a docker hub to run multiple nodes for different testing environments
- Dev Workflow
  - We want to be able to run tests in the background while doing other things
  - using "wait-for-\_\_\_.sh" scripts to wait for the services on the container to be running
    - useful for e.g. holding up application until db is connected
  - use docker-compose to run a separate service from application which runs tests with e.g. selenium
    - tell where tests are and expose endpoint/ports
- Devops Ready
  - we want to avoid situations where things work locally but not in pipeline
  - running UI tests in CI
    - faster feedback loops
    - simplifies debugging
    - avoid differences b/w local and CI execution
  - e.g. in Github Actions, you can add a step to the job to run tests with docker compose, then `--abort-container-exit --timeout 30`
- Extra Features
  - Video recording
    - dynamic grid: mount docker sock to container so anytime a test comes to the grid, we identify what browser to use, spin up a contianer, record video and logs and dump to mounted directory
    - set url to tell grid where to talk to Docker API/daemon
    - can upload video from GH actions to artifacts
  - "What about Safari and other Operating Systems?"
    - cross platform and browser testing is essential for optimal UI
    - extra feature allows you to connect to cloud vendor e.g. Sauce Labs, to relay test to other browsers/platofrms like Safari/macOS13, mobile testing, etc.
- Started 9 years ago, came from community, now sponsored by Docker
  - rely on community to make support for things like Chrome (not Chromium since it's not necessarily what users use) on Linux, etc.
  - Belief that open source drives innovation
- Recap:
  - less context switching
  - running test in parallel
  - cost reduction
  - quality boost through DevOps

### 15 Tips and Tricks to Improve Your Compose Experience

- `docker compose config`
  - `--images` prints out list of all images in compose file
  - `--services` prints out list of all services in compose file
- `docker compose up --dry-run`
  - shows what would happen if you ran the command
  - non-destructive operations
- `docker compose up --build`
  - If compose already has copy of image, it will not rebuild it typically. This forces it to rebuild (still uses build caches though unless specified otherwise)
  - can also be specified with `pull_policy: build` in compose file under the service
    - can also use e.g. `pull_policy: latest` to pull latest image
- `build > ssh` in compose file
  - ssh is often the authentication method used to pull from private repos
  - in build section you can provide the ssh key:
    - ```
      build:
        context: .
        ssh:
          - ssh_key: ["default"]
      ```
    - `RUN --mount=type=ssh,id=default git clone ...`
- `build > dockerfile_inline`
  - can specify dockerfile inline in compose file
  - ```
    build:
      context: .
      dockerfile_inline: |
        FROM alpine
        RUN apk add --no-cache git
        RUN git clone ...
    ```
  - not appropriate all use cases
- `depends_on > condition`
  - ```
    depends_on:
      db:
        condition: service_healthy
    ```
    - waits for service to start and be healthy before starting other services
    - default is `service_started`
  - seems useful for db that has started but not connected yet causing application to crash
- `depends_on > restart`
  - ```
    services:
      api:
        build:
        depends_on:
          db:
            restart: true
    ```
    - restarts service if something it depends on restarts
- `depends_on > required`
  - can fail api service if database service was not defined
  - ```
    services:
      app:
        build:
        depends_on:
          jaeger:
            required: false
      jaeger:
        image: jaegertracing/all-in-one
        profiles: ["tracing"]
    ```
- YAML Anchors
  - controversial language feature of YAML
  - can be used with compose
  - usefule when inside of compose file if you have set of common fields that you want to reuse (e.g. environment variables)
  - ```
    services:
      app:
        environment:
          <<: *common_env
          POSTGRES_USER: postgres
    ```
- `!reset`

  - when you use multiple compose files they merge maps/lists by default
  - `!reset` resets the map/lists
  - ```
    services:
      app:
        image: docker.io/library/alpine:latest
        build: !reset null
    ```

- `docker compose alpha viz`
  - visualizes compose file
  - `docker compose alpha viz --help` for more options
  - community contrbution
- `COMPOSE_EXPERIMENTAL_OTEL`
  - ```
    export COMPOTE_EXPERIMENTAL_OTEL=1
    export OTEL_EXPORTER_OTLP_ENDPOINT=http://localhost:4317
    docker compose up
    ```
  - OpenTelemetry
    - standard for collecting telemetry data
    - can be used to collect metrics, traces,
  - aggregate build data, figure out if health checks are misconfigured, debugging, etc.
  - note: still experimental
- `include`
  - use
    ```
    export COMPOSE_EXPERIMENTAL_GIT_REMOTE=1
    ```
    then
    ```
    include:
      - https://github.com/dockersamples/avatars.git#main
    ```
  - import a sub-project into your compose file
- `develop`
  - ```
    services:
      web:
        pull_policy: build
      build: .
      develop:
        watch:
          - path: web/
            target: /app
            action: sync
          - path: web/package.json
            action: rebuild
    ```
  - `docker compose develop` will watch for changes in the web directory and rebuild the image
  - just went GA

### New Developments in Compose

- significant chunk of Docker desktop usage
- open source tool
- analysis of multiple uses: homelab (rasp pi, tinkering, learning projects, etc.), simple production, complex production
  - For the latter, people are wrapping compose to try to be on par with tools like Kubernetes
- Compose really shines in "inner loop" (Code, Debug, Build and Test)
- 3 Main features:
  - "Watch"
    - reduce cognitive load of iterative loop
    - get all code changes into container so it can be reflected in the app (e.g. hot reload)
    - A few different options for better hot reload in e.g. React frontend
      - 'Sync' functionality
      - You can specify what to "Ignore" (e.g. node_modules/) so it doesn't immediately get synced back
    - Fast + Robust to account for branch chanegs etc.
    - Out now in GA
  - "Include"
    - Want to be flexible in how to structure complex projects
    - Allows you to bring together config files without having a depth of understanding about contexts for each config
    - example:
      - ```
        include:
          -my-compose-include.yaml
          # with serviceB declared
        services:
          serviceA:
            depends_on:
              - serviceB
              # use ServiceB directly
        ```
    - don't have to be as granualar with understanding all the relative like with `depends`
  - "Dry Run"
    - You often want to understand impact of what will happen when you run a compose command
    - `docker compose up --dry-run` to see what any given command will do
    - just about every command you can run can be done as a dry run
- Compose was rewritten from Python to Go
- Work done to make the spec more readable and able to be built upon in a responsible way
- Role of Compose in Docker Desktop being given new recognition and investment

### Streamlining CI/CD with Modern Container Builds

- Intro to Github Actions and key features
  - Key Features
    - Workflow: a set of automated steps defined in YAML files
    - Event: a specific activity that triggers a workflow
    - Runner: a server that runs the workflow
    - Jobs: units of work within a workflow
    - Actions: individual tasks with a workflow
- Docker Actions: Current state of official actions
  - 6 actions: `actions-toolkit`, `login-action`, `build-push-action`, `setup-qemu-action`, `setup-buildx-action`, `bake-action`, `metadata-action`
- Basic workflow
  - use `on` to trigger workflow
  - steps to login to docker hub and build/push image
  - can use `with` to specify environment variables
- Leverage cache
  - can speed up workflow by caching layers
  - Buildkit cache backends
    - inline
    - registry
    - local
    - s3
    - azblob
    - gha **(Github Actions)**
  - just need to include step "Set up Docker Buildx"
    ```
    uses: docker/setup-buildx-action@v3
    ```
    and then on other step with:
    ```
    cache-from: type=gha
    cache-to: type=gha
    ```
  - cache has size limit of 10GB shared across different caches in your repo
- Multi-platform build
  - can build for multiple platforms in one workflow
  - in `with:` section of a step include e.g. `platforms: linux/amd64,linux/arm64`
  - can take some time to emulate platofrms like arm64
    - Dockerfile and cross compilation can solve this
    - `FROM --platform=$BUILDPLATFORM golang:1.16-alpine AS build` and etc.
- Automating tags/labels: strategies to manage and automate tags and labels based on CI events
  - set tags in
    ```
    on:
      push:
        tags: - "v*"
      pull_request:
    ```
    then use below in
    ```
    - name: Docker meta
      id: meta
      uses: docker/metadata-action3v5
      with:
        images: crazymax/dockercon2023
    ```
  - more info: https://githiub.com/docker/metadata-action#tags-input
- Bake: Unleash power of Bake to simplify development workflows
  - Bake is a tool for building and deploying multi-arch container images
  - definition can be a HCL, JSON, or Compose file
  - multiple files can be specified with `--file` flag
    - Configuration is merged
    - variable block definition
      - use as build args in your Dockerfile
      - interpolate them in attribute vars in your bake file
- Secrets: Securely integrate build-time secrets withn your workflows
  - secrets are encrypted environment variables
  - can be passed to bake configuration
- Container-based wokflow

  - e.g. adding lint stage to workflow with:
    ```
    target 'lint' {
      target = "lint"
    }
    ```
    in bake with:
    ```
    - name: Lint
      with:
        targets: lint
    ```
    in workflow
  - Distributed builds

    - if you know for example a test can be a resource contraint, you can spread it out across multiple runners
    - can use `strategy` in workflow to specify `matrix` of different runners and assign to targets
    - instead of staging like this:

      ```
      prepare ---> validate (lint and test)

      ```

      we can do this to save time (using two runners:)

      ```
      prepare -----> validate(lint)
               \
                `----> validate (test)
      ```

## Day 2

### Keynote 2: Docker & AI

- Demo of Docker Generative AI stack
  - ollama to download and run Llama 2 model
  - vector and graph db by neo4j
  - python application powered by Lang chain
  - at first model doesn't have knowledge base to answer question so we want to add more context
    Enable RAG (retrieval augmented generation) mode to only use imported knowledge data instead of original training base
  - used Langsmith (tracing platform) to peek into difference between first and second chain
    - uses Neo4J to look up reference doccuments behind the scenes
- Learning center inside Docker Desktop has resources to build a similar GenAI stack
- Presentation from IKEA's Ingka gorup (retail arm)
  - with growing number of teams and interest in AI projects, started hitting constraints with computing resources
  - Docker solving the complexity of MLOps
    - conatinerized data science environments
      - place to experiment with different recommendation algorithms and datasets
      - deployment platform with Seldon Core
      - Prometheus performance monitoring
    - less than 10 days to have a deployable model
- Secure and Trusted Content for ML applications
  - 3 core problems: reporductibility, portablity, trust
  - Docker trusted content delivers dependable content from known sources for secure foundations, rather than using unknown images
    - e.g. Nginx, Alpine Linux, NodeJS, etc.
    - can use same trusted sources for AI/ML now
    - kept up to date with security patches and bug fixes
  - Docker verified publishers
  - Docker sponsored open source images
- Presentation from Western Ecosystems Technology env consulting (Wind energy)
  - Pilot study to use Computer Vision to analyze video of turbine impact with wildlife
  - low network conenctivity in the ocean, obviously
  - high computaitional load
  - Edge ML when you can't connect to your edge devices is pretty difficult
  - central problem is software environment consistency
    - you might send out your application to the device and come back 3 months later to find out it crashed because of a dependency issue - bad
  - many video streams to process in real time, and very little supervision but it worked on all devices
- Learning journey presentation from Stride
  - GenAI is supposedly the latest unified movement since Agile
  - 3 stages of safe experimentation
    - Fail fast and experiment, learn and play to find boundaries/rules
    - Build your own secure models, train with private data, etc. while other stakeholders are knocking on the door wanting tools
    - Finally, what is your informed opinion of what 'good' looks like? And how do you convince others?
- Docker AI Assistant
  - VS Code extension to open interactive notebook
  - "How do I dockerize my project?"
    - pulls up a Jupiter like notebook with interactive cells and documentation
      - `docker init walks through initial stages`
      - `docker compose up --build -d`
      - `docker compose down`
    - no longer have to write dockerfiles from scratch
  - "Summarize this project"
    - explains the main components of the project
    - gives recommendations to build
    - maybe you hit an error, it will scan context and give you recommendations to fix it
- Can be difficult to build AI/ML applications locally on a laptop
  - WebGPU allows shipping GPU support in browser, kinda brings this movement into the AI community
  - CPU can often max out, while GPU goes largely unused. If we offload some of that load to the GPU, it can be a lot faster and more efficient
  - still a work in progress, not available yet but "coming soon"
- Developer tools in the age of AI
  - moving to a future where we will have more machine-written code but that's ok because our job is to synthesize problems, create sollutions, innovate etc. Code has historically just been a tool to do so, as will using LLMs to accelerate this process.
  - We need to start transitioning from the goal of increasing productivity of an individual into addressing the complexity of a team
    - Not just to work more effectively indiividually but to work more cohesively with others
    - Docker Scout was kind of built to address this, to help the team have richer data on the state of all of the projects
  - PRs are extremely opinionated tools for teams to get code into a project, active feedback
  - Hopefully in the future LLMs can provide more active nudges (like a PR) that can analyze values of teams to nudge in different directions
    - e.g. my team values code quality above all, or rapid shipping, security, etc.
  - we need to embrace these tools going forward. DEvelopers are hisotrically very effetive tool users so don't be afraid to shift and adopt.
  - move from "just writing code" mindset into more of a problem solving mindset

### Getting Started with Wasm, Docker, and Kubernetes

- Workshop link: https://github.com/nigelpoulton/dockercon2023-wasm-lab
- WebAssembly is a binary instruction format for a stack-based virtual machine
  - can be run in a browser
  - can be run in a server
  - can be run in a container
- Three waves of cloud computing
  - Virtual machines > Conatiners > WebAssembly
- `spin new`, `spin build`, `spin up`
- Kubernetes is a high-level orchestrator to run tasks over nodes, uses other tools to run containers (such as containerd)
- Pre-reqs
  - up to date Docker Desktop
  - Docker Hub account
  - Rust (Python is also supported)
  - Fermyon Spin
  - kubectl (kubernetes controller)
  - k3d
- Build and compile the Wasm app
  - Docker Desktop settings, Features in dev, 'Use containerd' and 'Enable wasm"
  - using wasm we can compile to an machine (that has wasm compiler) which is more portable and universal than containers
  - `spin new`
    - select a template e.g. http-rust
    - enter a name e.g. dockercon
  - `cd dockercon`
  - `lib.rs` is the main file
    - make some changes to body
  - `spin.toml` is the config file that tells how to run application
  - `spin build` compiles the application as webassembly binary
  - then `dockercon.wasm` is the web assembly application
  - to test `spin up` which will bring up application and say where it's listening
  - Now to run in Docker and Kubernetes:
- Package wasm as OCI image
  - create new Dockerfile
    - 3 line boilerplate dockerfile in the workshop repo
      - ```
        FROM scratch
        COPY /target/wasm32-wasi/release/dockercon.wasm .
        COPY spin.toml .
        ```
  - change `spin.toml` file to remove leading path in source
  - `docker buildx --platform wasi/wasm --provenance=false -t nigelpoulton/docker-wasm:spin-0.1 .`
    - (build on lateste versions will work)
  - ```
    docker run -d \
    --runtime=io.containerd.spin.v1 \
    --platform=wasi/wasm \
    -p 5005:80 \
    nigelpoulton/docker-wasm:spin-0.1 /
    ```
  - go to port 5005, should be running
- Run it on Kubernetes
  - `docker push nigelpoulton/docker-wasm:spin-0.1` etc.
  - should be visible in docker hub now, architecture wasi/wasm
  - ```
    k3d cluster create wasm \
      --image ghcr.io/deislabs/containerd-wasm-shims/examples/k3d:v0.9.1 \
      -p "8081:80@loadbalancer" --agents 2
    ```
  - single kubernetes cluster with a single control plane node, port with load balancer, and 2 worker nodes
- Kubernetes Node config
  - `kubectl get nodes` should show the 3 node cluster
  - Kubernetes offloads container startup to containerd, which offloads to shim. Kubernetes doesn't care what's actually doing the work so we can use Wasm shims
  - let's just check for shims:
    - `docker exec -it k3d-dc-agent-0 bash`
      - `ls /bin | grep containderd-`
        - look for shims
  - `kubectl label nodes k3d-dc-agent-1 wasm=yes` labels the node
  - now we need a runtime class
    - available in repo `rc.yaml`
  - create the app.yaml
  - then apply:
  - `kubectl apply -f app.yaml`
- main reason we do all of this is because while Docker is 'portable' in that it's small and easy to transport images, it isn't truly portable because it's tied to a specific architecture. Wasm fixes this because it can be run on any architecture that has a wasm runtime.

### Things You Always Wanted to Know About Building Platforms

- Why is it so hard to build a platform?
  - cognitive load, constraints and dependencies
- A platform is a set of interfaces that simplifies tasks
- We build software by delineating conventions
- Component (services, applications)
- Context (environment, where you're dpeloying)
- Target (things needed to run a component in a context, how we transform things)
- Why is Kubernetes so complex
  - how many settings are in wordpress? (55)
  - deploying wordpress in kubernetes, how many settings are there? (291)
  - 5 times more settings for deploying than to configure application
- Golden Paths (things we can use to go fast)
  - the tool does nothing if it doesn'tfit your workflow
  - if your platform owns the golden path, it's going to be a bottleneck for you
- Platform as a Product
  - Devops tries to remove friction between Dev and Ops
  - Platform tries to remove friction by creating a new set of interfaces
- Ivan's rules to build a platform
  - Composability
  - Reproducibility
  - Automation
  - Flexibility (you know there will be exceptions or unplanned cases)
- Additional tips:
  - don't say no
  - define standard interfaces
  - define standard processes
  - automate every single step
  - producers and consumers (roles and repsonisbilitites)
  - define contracts
    - producer owns the implementation (and runs it)
- Platform engineering is clsoer to _user experience_ than infrastructure
- Self service is about provideing a fast-track lane, not about reducing options
- We don't build a platform to do more, we build it to do less
  - we want to offload
- Problems:
  - your platform is a new dependency
    - how easy is it to adopt that dependency
  - how many explicit and explicit constrainst are there
  - how much do customers need to know?
- Platform engineering is the new devops
- Summary:
  - growing scope causes unrealistic expectations
  - takes time and effort to resolve

### AI Anytime, Anywhere: Getting started with LLMs on your Laptop Now!

- AI usage has exploded in the last couple years
  - users are asking and trusting without verificiation
  - people are submitting their own data, (e.g. allowing Obsisdian note-taking to be indexed)
    - personalized data has personalized results!
    - but also can have bad outcomes like your info unintentionally becoming part of the model and shared with others
    - can also potentially skew future results
  - so a lot of organizations are creating policies restricitng use of these hosted tools
  - possible solution is going local
    - many use [llama.cpp](https://github.com/ggerganov/llama.cpp)
    - this session focuses on ollama.ai
- LLMs (Large Language Models) are basically contextual text prediction
  - one of the main pieces is a token (most common words or parts of words)
    - tokens are stored as numeric values, not the "words" themselves
  - weights and biases are used to link tokens together on thousands of dimensions
  - quantization: weights are stored as 32bit floats, which can lead to HUGE filesizes. Quantization groups the weights into buckets and stores them as (e.g.) 2 to 8bit integers which still works surprisingly well
- Hugging Face provides a lot of pretrained models you can use
- Demo

  - Download and Install Ollama from their site
  - `ollama run llama2`
  - then you can enter prompts and it will respond. Context is kept for successive prompts
  - llama2 is one of many models you can use
  - you can create your own modelfiles similar to a Dockerfule e.g:

    ```
    FROM llama2

    PARAMETER temperature 1.0

    SYSTEM """
    You are a product manager at a tiny software company who only speaks english. When you respond, only offer a single open question
    """
    ```

  - `ollama create expm`
  - `ollama run expm`
  - ollama docs on [github](https://github.com/jmorganca/ollama/tree/main/docs) explain RESTful endpoints
  - there is also a [python client](https://github.com/jmorganca/ollama/blob/main/examples/python/client.py).

- There is now an official Ollama docker image: https://ollama.ai/blog/ollama-is-now-available-as-an-official-docker-image
- 8RB Ram recommended for 7 million parameters, every model is different
- generating responses is based on GPU resources
- Question: Can you have multiple SYSTEM prompts in your model file?
  - No, only one system prompt can be directly input per model, but you can process conditional logic before passing to the model with your python/node scripts

### Debugging Innovation

- Debugging a container can be difficult, often you are missing your normal toolset due to the containerized environment
  - User experience in Docker exec is not great, even according to the Docker team
- Docker Desktop has a new feature called "Debug" which allows you to debug your application in a container
  - available in the extension marketplace as [Docker Labs Debug Tools](https://open.docker.com/extensions/marketplace?extensionId=docker/labs-debug-tools-extension)
- anything that exists in the nix universe can be brought into DLD (docker labs debug)
- nano and vim come out of the box but you can install e.g. tree and so on
- slim containers (e.g. Alpine, scratch)
  - great until you need to debug them because they don't have shell or anything in them
- Pretty cool, seems like a lightweight alternative to using VS Code's Remote Explorer/Docker extensions
- hopefully allows you to debug at the entrypoint level and such
- can also get a shell into an image, doesn;t have to be a container. e.g. `dld nginx shell`
  - acts like a sandbox environment, changes will be lost when you exit
  - made to troubleshoot or poke around, not _build_ images
- `entrypoint --print` shows the command that will be run when you execute the image
  - you can also do `entrypoint --lint` to check for errors
- still experimental and an extension but hopefully will be added to Docker Core
- How Docker Debug works
  - running containers are just processes
  - can we run a process (our debug chell) that sees the same things the running container sees?
  - How can we get debug tools in our container? We don;t want to actually change our container or copy anything into there
    - we add a second "sidecar" container level that has all the tools
    - uses Nix:
      - no cluttering of /lib or /var/lib
      - huge existing package repository
- What's next?
  - Kubernetes
  - we want to be able to use this debugging experience anywheere
  - cleanup
  - Integrating in Docker Desktop (docker shell)
  - Standalone plugin (docker shell as cli plugin release)
