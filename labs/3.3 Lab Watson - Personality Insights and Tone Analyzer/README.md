<img src="./images/VisualRecognition.png" width="20%"/>

# 3.3 Lab Watson - Personality Insights and Tone Analyzer

Personality Insights service allows to gain insight into how and why people think, act, and feel the way they do. This service applies linguistic analytics and personality theory to infer attributes from a person's unstructured text. Tone Analyzer service uses linguistic analysis to detect joy, fear, sadness, anger, analytical, confident and tentative tones found in text.


# Objective

In the first part on the lab, you will access a Personality Insights quick demo so as to understand the Personality Insights service and its use in an application. With this service you can gain insight into how and why people think, act, and feel the way they do. This service applies linguistic analytics and personality theory to infer attributes from a person's unstructured text. In the second part of the lab, you will create a Watson Personality Insights service and then you will learn how to call it through cURL commands.
You will then access Tone Analyzer quick demos so as to understand the Tone Analyzer service and its use in an application. You will create a Tone Analyzer service and you will then a create a Node-RED application that uses this created service.


+ How to use Watson Personality Insights
+ How to use Watson Tone Analyzer
+ Integrate the service in a web app


# Pre-Requisites

+ Get an IBM Cloud Platform account in the US region (https://cllebrun.github.io/labs/0_Registration/), or use an existing account.


# Steps

1. Personality Insight Demo
1. Personality Insight Service
1. Tone Analyzer Service


# Step 1 - Personality Insight Demo

1. Access the Personality Insights quick demo at the following url: https://personality-insights-demo.ng.bluemix.net/

   <img src="./images/PI-demo.png"/>

   Personality Insights service allows to gain insight into how and why people think, act, and feel the way they do. This service applies linguistic analytics and personality theory to infer attributes from a person's unstructured text.

   The quick demo application allows to analyze text from three sources:
  - Tweets and replies from several people (Oprah Winfrey, LeBron James, Don Francisco, Pope Francis, Mohamed Aboutrika, Sefat Farid Yu Darvish and Sandara Park)
  - Text from several people (Barack Obama, Gandhi and Natsume Soseki) or your own text (more than 100 words)
  - Your own tweets and replies

1.  For tweets and replies analysis, first select a twitter account and click on the Analyze button.
  You get the results of the analysis in the Output section.
  <img src="./images/output-demo.png"/>


  - First output is a summary of the personality.
  - On the right, you can see the consumption preferences.

  The Personality Insights service infers consumption preferences based on the results of its personality profile for the author of the input text. From existing literature, IBM identified 104 consumption preferences that have proved to be correlated with personality. These include preferences that are related to shopping, movies, music, and other categories. IBM then created a psychometric survey to assess an individual's inclination for each consumption behavior.

  IBM obtained responses to its survey from about 600 individuals for whom it also had Twitter data (more than 200 self-authored tweets for each user). IBM submitted the tweets to the service to gather a personality profile for each individual. It then built a classifier for each consumption preference, where the input feature set was the personality information.

  For inclusion with the service, IBM selected only those consumption preferences forwhich personality-based classification performed at least 9 percent better than random classification. Of the original 104 preferences, 42 satisfied this criterion and are exposed as consumption preferences by the service.

  Here is the list of the consumption preferences returned by the service:
  - Shopping preferences: Shopping preferences indicate the author's interest in different types of purchases, the extent to which the author's purchasing habits are influenced by different external sources, and the author's spending habits. This category has 12 preferences.
  - Movie preferences: Movie preferences indicate the author's interest in different types of movies. This category has 10 preferences.
  - Music preferences: Music preferences indicate the author's interest in different types of music and whether the author enjoys playing music. This category has nine preferences.
  - Reading and learning preferences: Reading and learning preferences indicate the author's likelihood to read, the author's motivation for reading, and the types of content the author enjoys reading. This category has five preferences.
  - Health and activities preferences: Health and activity preferences indicate the author's interest in healthy foods and physical activity. This category has three preferences.
  - Entrepreneurship preferences: Entrepreneurship preferences indicate the author's interest in starting a business. This category has one preference.
  - Environmental concern preferences: Environmental concern preferences indicate the author's interest in the environment. This category has one preference.
  - Volunteering preferences: Volunteering preferences indicate the author's interest in volunteering for social causes. This category has one preference.

  Then you can find the models reported by the service:
  - Personality: based on the Big Five model. Big Fives one of the most studied of the personality models that were developed by psychologists Costa and McCrae(1992),and Norman(1963). It is the most widely used personality model to describe how a person generally engages with the world. The service computes the five dimensions and thirty facets of the model. The dimensions are often referred to by the mnemonic OCEAN, where O stands for Openness, C for Conscientiousness, E for Extraversion, A for Agreeableness, and N for Neuroticism. (Because the term Neuroticism can have a specific clinical meaning, the service presents such insights under the more generally applicable heading Emotional range.)For each dimension you can get details by clicking on the arrow sign next to it.
  - Consumer Needs: Needs are an important aspect of human behavior. Research literature suggests that several types of human needs are universal and directly influence consumer behavior (Kotler and Armstrong(2013) and Ford(2005)). The twelve categories of needs that are reported by the service are described in marketing literature as desires that people hope to fulfill when they consider a product or service.
  - Values: Values convey what is most important to an individual. They are "desirable, trans-situational goals, varying in importance, that serve as guiding principles in people's lives" (Schwartz, 2006). Schwartz summarizes five features that are common to all values:
    - Values are beliefs.
    - Values are a motivational construct.
    - Values transcend specific actions and situations.
    - Values guide the selection or evaluation of actions, policies, people, and events.
    - Values vary by relative importance and can be ranked by importance.

    The service computes the five basic human values that were proposed by Schwartz and that were validated in more than twenty countries (Schwartz, 1992).You can get an explanation of each characteristic simply by hovering over it.



2.  Get a sunburst visualization by clicking on the “View personality traits in sunburst visualization” link.

  <img src="./images/chart-demo.png"/>


3. Feel free to test with your own Twitter account !

# Step 2 - Personality Insight Service

1.  On the IBM Cloud console, navigate to the catalog and look for the **Personality Insights** service. Click on the service tile.

  <img src="./images/PI-service.png"/>

1. Choose the Dallas region, the Lite plan and click **Create**. The service instance is created, and the service dashboard page opens automatically.

  <img src="./images/PI-creation.png"/>

1.  On the Personality Insights service dashboard page, click on Manage.
1.  On the Manage tab, click Show Credentials to view your credentials.
1.  Copy the API Key and URL values.

  The examples described in this document use the curl command to call methods of the HTTP interface. Make sure that you have the curl command installed on your laptop. If not already installed, install the version for your operating system from curl.haxx.se Install the version that supports the Secure Sockets Layer (SSL) protocol. Make sure to include the installed binary file on your PATH environment variable. When you enter a command, replace {apikey} and {url} with your actual API key and URL. Omit the braces, which indicate a variable value, from the command.

  **Send plain text input and receive basic JSON output**

  This first example passes the plain text file profile.txt to the POST /v3/profile method and requests a JSON response.
1.  Download the sample file profile.txt

1.  Issue the following command to send the file to the /v3/profile method and request a JSON response.

  a.  The Content-Type header specifies that the input is plain text, text/plain. The charset parameter included with the header identifies the character encoding of the input text.

  b.  The Accept header specifies application/jsonto indicate that JSON output is requested.

  c.  Replace {apikey} and {url} with your information.

  d.  Modify {path_to_file} to specify the location of the profile.txtfile.

  **Linux version of the command:**
  ```
   curl -X POST -u "apikey:{apikey}" \--header "Content-Type: text/plain;charset=utf-8" \--header "Accept: application/json" \--data-binary @{path_to_file}profile.txt \"{url}/v3/profile?version=2017-10-13"
   ```

   **Windows version of the command:**
   ```
   curl -X POST -u "apikey:{apikey}" --header "Content-Type: text/plain;charset=utf-8" --header "Accept: application/json" --data-binary "@{path_to_file}profile.txt" "{url}/v3/profile?version=2017-10-13"
   ```
   The service returns a JSON Profile object that includes basic metadata such as the number of words in the input, the language model with which the input was processed, and any warnings associated with the input. The profile includes information about the Big Five personality, Needs, and Values characteristics for the author as inferred from the input text. The service reports a percentile, or normalized score, for each characteristic. The service computes the percentile by comparing the author's results with the results from a sample population.

   **Send JSON input and receive detailed JSON output**

   In this example, a JSON file is passed to the /v3/profile method, again requesting a JSON response. The example requests consumption preferences and raw scores for a more detailed analysis of the input.

1. Download the sample file profile.json. This file contains a collection of Twitter messages.
1.  Issue the following command to send the file to the /v3/profile method. The example specifies application/json for the Content-Typeand Accept headers; the charset parameter is not needed for JSON input. The example sets the consumption_preferencesand raw_scoresquery parameters to true.

  **Linux version of the command:**

  ```
  curl -X POST -u "apikey:{apikey}"\--header "Content-Type: application/json"\--header "Accept: application/json"\--data-binary @{path_to_file}profile.json \"{url}/v3/profile?version=2017-10-13&consumption_preferences=true&raw_scores=true"
  ```

  **Windows version of the command:**
  ```
  curl -X POST -u "apikey:{apikey}" --header "Content-Type: application/json" --header "Accept: application/json" --data-binary @{path_to_file}profile.json "{url}/v3/profile?version=2017-10-13&consumption_preferences=true&raw_scores=true"
  ```
  The service returns a JSON profile that includes the metadata and characteristics returned with the previous example. For each characteristic, the service also includes a raw_score, which represents the author's score for the characteristic based solely on the input text, without comparing the results to a sample population.

  Because the input content includes timestamps, the service also reports behavioral characteristics. These are temporal characteristics that indicate the percentageof the content items that were created on each day of the week and hour of the day.

  The service also reports scores for its collection of consumption preferences. The scores indicate the author's likelihood to prefer different products, services, and activities based on the inferred characteristics.

  **Send JSON input and receive detailed CSV output**

  This example is similar to the previous one: it passes the same JSON content and requests the same results. But this example specifies text/csv for the Accept header to request the response in comma-separated values (CSV) format. It uses the --output option of the curl command to direct the results to a file named profile.csv. The example sets the csv_headers query parameter to true to request that column headers be returned with the output.

  Issue the following command to send the JSON file to the /v3/profile method. The Content-Type header identifies the input content as application/json, and the Accept header requests CSV output, text/csv:

  **Linux version of the command:**

  ```
    curl -X POST -u "apikey:{apikey}"\--header "Content-Type: application/json"\--header "Accept: text/csv"\--data-binary @{path_to_file}profile.json \--output profile.csv \"{url}/v3/profile?version=2017-10-13&consumption_preferences=true&raw_scores=true&csv_headers=true"
    ```
    **Windows version of the command :**
    ```
    curl -X POST -u "apikey:{apikey}" --header "Content-Type: application/json" --header "Accept: text/csv" --data-binary "@{path_to_file}profile.json" --output profile.csv "{url}/v3/profile?version=2017-10-13&consumption_preferences=true&raw_scores=true&csv_headers=true"
    ```
# Step 3 - Tone Analyzer Service

# Resources

For additional resources pay close attention to the following:

- [Watson Personality Insights Documentation](https://cloud.ibm.com/docs/services/personality-insights?topic=personality-insights-gettingStarted)

- [Watson Personality Insights API Reference](https://cloud.ibm.com/apidocs/personality-insights)

- [Watson Tone Analyzer Documentation](https://cloud.ibm.com/docs/services/tone-analyzer?topic=tone-analyzer-about&_ga=2.9548789.1595110995.1575383823-679962596.1538488997&cm_mc_uid=66302025876115544728192&cm_mc_sid_50200000=78316381575389656642&cm_mc_sid_52640000=41254171575389656644#about)

- [Watson Tone Analyzer API Reference](https://cloud.ibm.com/apidocs/tone-analyzer?_ga=2.175141858.1595110995.1575383823-679962596.1538488997&cm_mc_uid=66302025876115544728192&cm_mc_sid_50200000=78316381575389656642&cm_mc_sid_52640000=41254171575389656644)
