# Jupyter-uid

<img width="1092" alt="image" src="https://github.com/user-attachments/assets/5f735528-a104-4ec1-8455-de1f7eac44c7" />


Running Jupyter as a Specific User in Run:AI with Custom UID/GID Settings
When setting up a Jupyter environment in Run:AI, you may want to run the container as a specific user to ensure proper permissions, security, and access to resources. The screenshot shows the "Security" section of the environment setup, where you can configure the UID, GID, and supplementary groups for the container.

Understanding the Security Settings
From the Image (Default Option Selected): This means the container will use the UID, GID, and supplementary groups defined in the container image. For Jupyter images, this is often the default user (e.g., jovyan in official Jupyter Docker images, with a UID of 1000 and GID of 100).

Custom: This option allows you to specify a custom UID, GID, and supplementary groups. This is useful if you need to align the container's user with a specific user on the host system, especially for shared storage or specific permission requirements.

Steps to Run Jupyter as a Specific User
Determine the Desired User and Group IDs:
If you want Jupyter to run as a specific user, you need to know the UID and GID of that user on the host system.

id -u <username>  # For UID
id -g <username>  # For GID


Configure the Security Settings in Run:AI:
In the "Security" section (as shown in the screenshot), select the "Custom" option instead of "From the image."

Enter the UID (e.g., 1001) and GID (e.g., 1001) for the user you want the container to run as.

If the user belongs to additional groups (supplementary groups), you can specify those as well. For example, if myuser is part of a group with GID 2000, you can add that to the supplementary groups.

Create the Environment:
Once you’ve configured the security settings, click "Create Environment" (as shown in the screenshot) to finalize the setup.

Run:AI will create a container with the specified UID/GID, ensuring Jupyter runs as the desired user.

Verify the Setup:
After the environment is created, launch Jupyter and verify the user by running a terminal command inside Jupyter:

id

This should return the UID and GID you specified (e.g., uid=1001(myuser) gid=1001(myuser)).

Why This Matters
Running Jupyter as a specific user is important for:
File Permissions: If Jupyter needs to access shared storage (e.g., NFS mounts), the UID/GID must match the user on the host system to avoid permission issues.

Security: Running as a non-root user with a specific UID/GID reduces the risk of privilege escalation.



