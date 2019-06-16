# Cloud IAM
IAM - Identity and Access Management

ALlows us to create and manage permissions on GCP through a single system of access control like creatings users with different previliges and access control (Owner and viewer roles)

## Adding new Members
1. Go to **Navigation menu > IAM & Admin > IAM**
1. Add a new user using the **+ADD** Button and assign project roles relevant to the user like **Browser, Editor, Owner or Viewer**

Roles

[GCP Roles Documenttaion](https://cloud.google.com/iam/docs/understanding-roles#primitive_roles)

Category|Role
--|--
Viewer | Permissions for read-only actions that do not affect state, such as viewing (but not modifying) existing resources or data.
Editor |All viewer permissions, plus permissions for actions that modify state, such as changing existing resources.
Owner | All editor permissions and permissions for the following actions: 1. Manage roles and permissions for a project and all resources within the project. 2. Set up billing for a project.
Browser | Read access to browse the hierarchy for a project, including the folder, organization, and Cloud IAM policy. This role doesn't include permission to view resources in the project.