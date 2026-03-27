---
author: "Wren Howell"
title: "Analyzing Suspicious Containers on Hosts: A Sha-Hulud Case Study" 
date: 2025-12-15
description: "Investigating Containers"
tags: ["Incident Response, Container Security"]
thumbnail: https://cached.imagescaler.hbpl.co.uk/resize/scaleWidth/952/cached.offlinehbpl.hbpl.co.uk/news/RDN/Ashippingcontainerfullofplasticwasteforexport-landscape.ENDSReport_TessColley-fotor-20250916114748.jpg
---

Supply chain compromises like Shai-Hulud are nightmares because remediation has to happen at every level of the affected machines. Even if remediation is done at the first tier, if it doesn't occur at every level after that, there is still a risk of compromise—especially when a popular tool like npm packages gets hit.

## What is Shai-Hulud 2.0?

Shai-Hulud 2.0 is a supply chain worm that targets the npm ecosystem by infecting legitimate packages with malicious code. Once a developer installs a compromised package, the worm steals sensitive credentials such as npm tokens, GitHub tokens, and cloud keys from local machines and CI/CD pipelines. It then uses those stolen credentials to automatically compromise and republish other packages—allowing it to propagate rapidly like a worm.

Many researchers have published IOCs associated with Shai-Hulud 2.0, and identifying them on hosts by looking up hashes is relatively trivial. But if the affected Shai-Hulud npm package is not on a traditional host (e.g. containers), triaging looks a little different.

I've wanted to write a blog post on how to triage potentially malicious containers for a long time, so I'm using this Shai-Hulud incident to do so. This guide is a walkthrough on how to investigate potentially malicious containers using the IOCs from Shai-Hulud as a guide. This walkthrough assumes that the container is running on a host and is a Linux-based container. 

Please note that this is not a remediation guide for organizations affected by Sha-Hulud. Sha-Hulud IOCs are used solely as examples to demonstrate how to investigate container artifacts. More detailed reports on Sha-Hulud are linked in the resource section. 

## Important Distinctions

**Images vs. Containers:**
- **Images** are read-only templates that contain everything needed to run something. An image is like a recipe to make a cake.
- **Containers** are running instances of the image. The container is the actual cake.

Note: Throughout this guide, images and containers may be used interchangeably, but keep this distinction in mind.

## Step 1: Getting the Malicious Container from the Host to Your Analysis Machine

First, find the running containers on the host by using:

```bash
docker ps -a
```

This command lists all containers (both running and stopped). The `-a` flag shows all containers, not just running ones.

Once you've identified the container of interest, save its state into a `.tar` file:

```bash
docker export <container_id> -o malicious_container.tar
```

Or, if you want to save the image instead:

```bash
docker save -o malicious_image.tar <image_name>:<tag>
```

**Note:** `docker export` exports the container's filesystem, while `docker save` exports the image with all its layers and metadata. For forensic analysis, `docker save` is often preferred as it preserves more information.

## Step 2: Transfer the .tar File to Your Analysis Machine

Transfer the `.tar` file to your analysis machine. If you use a EDR like Crowdstrike, Defender, SentinelOne, or Semantic all you have to do is download the tar file on the analysis machine. 

## Step 3: Load the Container/Image on Your Analysis Machine

Once the `.tar` file is on your analysis machine, load it:

If you used `docker save`:

```bash
docker load -i malicious_image.tar
```

If you used `docker export`, you'll need to import it as an image:

```bash
docker import malicious_container.tar malicious_container:analysis
```

## Step 4: Run the Container and Analyze

Now run the image in an isolated environment so you can analyze the files:

```bash
docker run -it --rm --network none <image_name>:<tag> /bin/bash
```

**Flags explained:**
- `-it`: Interactive terminal
- `--rm`: Automatically remove the container when it exits
- `--network none`: Isolate the container from the network (this is a safeguard to make sure the malware does not connect to the network)
- `/bin/bash`: Start a bash shell 

**Alternative: Analyze without running the container**

For safer analysis, you can also inspect the filesystem without actually running the container:

```bash
# Create a container from the image without starting it
docker create --name analysis_container <image_name>:<tag>

# Export the filesystem
docker export analysis_container -o filesystem.tar

# Extract and analyze
tar -xf filesystem.tar -C ./analysis_directory/

# Clean up after analysis is done
docker rm analysis_container
```

## Step 5: Look for Shai-Hulud IOCs

Now that you're in the shell of the container (or have extracted the filesystem), you can look for potential IOCs associated with the Shai-Hulud malware(any of the packages affected by Shai-Hulud like AsyncAPI):

```bash
# Check for suspicious npm packages in node_modules
find / -name "malicious_node_modules_like_AsyncAPI" -type d 2>/dev/null
```

## Conclusion

Supply chain attacks like Shai-Hulud are tricky to contain, and many companies do not have adequate visibility to containers. I hope this guide serves as a starting point, if there is ever a need to investigate potentially compromised containers.

Resources 
- https://www.trendmicro.com/en_us/research/25/k/shai-hulud-2-0-targets-cloud-and-developer-systems.html

Affected Sha-Hulud 2.0 NPM packages published by Wiz
- https://github.com/wiz-sec-public/wiz-research-iocs/blob/main/reports/shai-hulud-2-packages.csv 




{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>

{{< /css.inline >}}
