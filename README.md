
# Docker Volume Example with Alpine

## Project Overview
This project demonstrates how to use Docker Volumes to persist data across container restarts and removals. We use an Alpine Linux container, write some data to a mounted Docker Volume, and verify the data persists even after the container is deleted.

---

## 🚀 Setup Instructions

### Step 1: Create a Docker Volume
To create a Docker Volume, run the following command:
```bash
docker volume create my-alpine-volume
```

Verify the volume is created:
```bash
docker volume ls
```

---

### Step 2: Run an Alpine Container with the Volume
We will mount the volume to `/data` inside the container:
```bash
docker run -it --name alpine-container -v my-alpine-volume:/data alpine /bin/sh
```

- `-v my-alpine-volume:/data`: Mounts the Docker volume to `/data`.
- `--name alpine-container`: Names the container.
- `-it`: Interactive mode with shell access.

---

### Step 3: Write Data to the Volume
Inside the container shell, run:
```sh
cd /data
echo "Hello from Docker Volume!" > testfile.txt
cat testfile.txt
```

You should see:
```
Hello from Docker Volume!
```

---

### Step 4: Stop and Remove the Container
Exit and remove the container:
```sh
exit
docker stop alpine-container
docker rm alpine-container
```

---

### Step 5: Run a New Container with the Same Volume
We will spin up a new Alpine container with the same volume:
```bash
docker run -it --name alpine-container-2 -v my-alpine-volume:/data alpine /bin/sh
```

Navigate to `/data` and check the contents:
```sh
cd /data
ls
cat testfile.txt
```

You should still see:
```
Hello from Docker Volume!
```

---

## 📝 Result
The data is persisted because it was stored in the Docker Volume. Even if the container is removed, the data remains available.

---

## 🧹 Cleanup
To clean up all resources:
```bash
docker stop alpine-container-2
docker rm alpine-container-2
docker volume rm my-alpine-volume
```

---

## 📧 Contact
For any questions or issues, please contact [your-email@example.com](mailto:your-email@example.com).
