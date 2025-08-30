# Conversion Rate

## Background

This is one of several projects to hand in order to get my data science diploma. The Convertion Rate project is one of three projects that validate the Machine Learning module.\
See "Conversion_rate_challenge.ipynb" for more.

## Tracking Server

[The MLFlow tracking server](https://aengusbl-conversion-rate-tracking-server.hf.space)

Please note that the name of the "test_r2" column is a mistake I made when setting up the MLFlow logging: The scores are all F1 scores, but I could not change the name of the column after the fact, and I decided that it would be more confusing to have two score columns in the tracking server, so I left the name there for the sake of consistency. Sorry for any confusion this may cause.

### Tracking Server Setup

1. In Hugging Face Spaces, create a space. You are then presented with a `git clone` command. A Hugging Face Space runs off of a Git repository and refreshes automatically when a push is performed on said repository. Run the `git clone` command in the location you want the repository to be.
2. In the folder that is then created, add the contents of the "tracking_server" folder of this here GitHub repository.
3. For the space to function properly, you need to add some secret values to the space. To add secrets, go to your Hugging Face space, click "Settings", and scroll down to "Variables and secrets".
4. Some of the secret values you will need come from AWS. Create an account if you don't have any.
5. In AWS, create an Amazon S3 bucket.
6. In AWS create an IAM user that has access to this S3 bucket. Make sure to keep this user's credentials.
7. Go to neon.com, create an account and create a new project.
8. Go back to Hugging Face, and add the secret values as given here. The parts in uppercase are the names of the secrets, and the parts after the arrows are the values of the secrets. Do not include the arrows.
    * AWS_ACCESS_KEY_ID -> This is the access key ID for the IAM user you created.
    * AWS_SECRET_ACCESS_KEY -> This is the secret access key for the IAM user you created.
    * ARTIFACT_STORE_URI -> This is the resource ID of the S3 bucket you created. It should look like "s3://the-name-of-your-bucket".
    * BACKEND_STORE_URI -> This is the link you find after "psql" when pressing "Connect" in the project you created at neon.com. Make sure you got the version of the link that isn't partially hidden with asterisks.
9. The space should be working.
10. You can now set up your access to the MLFlow tracking server: Create a file called ".env" outside of the folders created with the `git clone` command, and add to it the four secrets we set above. Each line should look like `SECRET_VALUE=paste_the_value_here`. Also add to it `TRACKING_SERVER_URL=link to your MLFlow space`.
11. Train a model while implementing logging through MLFlow, as seen in model_research.ipynb.