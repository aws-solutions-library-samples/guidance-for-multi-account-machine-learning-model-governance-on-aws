# Building an example Amazon QuickSight dashboard for Model Governance

Among the possible visuals for Model Governance, we can mention:

- Use case properties:
    
    1. List use cases by stage 

- Model properties:
    
    2. List models by LoB, stage, risk, status
    3. Model validation metrics
    4. Model audit information

- Endpoint properties:
    
    5. Model monitoring metrics

We will quickly introduce Amazon Quicksight and then show how to realize the first 2 visuals.

## Exploring the environment

A good starting point on the subject is the extended [Amazon QuickSight documentation on Visualizing data](https://docs.aws.amazon.com/quicksight/latest/user/working-with-visuals.html).

- When logging in inside Amazon Quicksight for the first time, the console will look similar to the screenshot below:

    ![quicksight](<Screenshot 2024-11-15 213113.png>)

- By clicking on "Datasets" on the left pane, you should see the newly created datasets based on DynamoDB connector through Amazon Athena

    ![quicksight](<Screenshot 2024-11-15 213133.png>)

- When clicking on a datasets, additional information are shown
    
    ![quicksight](<Screenshot 2024-11-15 213201.png>)


- By clicking on "EDIT DATASET", a detailed view of the dataset Fields, their type and example data are shown
    
    ![quicksight](<Screenshot 2024-11-15 214318.png>)

- To use the dataset within an Analysis, click on "USE IN ANALYSIS" in the dataset view. This will open an Analysis where the Layout settings will pop up. We can click on "CREATE"
    
    ![quicksight](<Screenshot 2024-11-15 214353.png>)

## List use cases by model stage 

- To start building visualizations, it is sufficient to drag and drop a dataset Field into the empty canvas. For example `modelstage`. This way a horizondal histogram is created showing the distribution of the model stages. It can become a vertical histogram by selecting the corresponding Visual.
    
    ![quicksight](<Screenshot 2024-11-15 214744.png>)

- To add more depth to the displayed information, we can group the data by `usecasename`. The different use cases will have different colors.
    
    ![quicksight](<Screenshot 2024-11-15 215128.png>)

## List models by Line of Business

- Similarly to above, we can click on a void space to add an empty canvas, and drag and drop the Field `modellob` representing the model Line of Business, and group the data according th `modelpackagearn` (i.e. the unique ID of each model version)
    
    ![quicksight](<Screenshot 2024-11-15 215408.png>)

## Publishing the dashboard

- By clicking on the button "PUBLISH" on the top right of the screen, a dashboard will be created containing all the canvases created in the analysis
    
    ![quicksight](<Screenshot 2024-11-15 215640.png>)

- By clicking on each item in the histograms, detailed informations are shown
    
    ![quicksight](<Screenshot 2024-11-15 215658.png>)

