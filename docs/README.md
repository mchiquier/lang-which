# README:

## Steps of Original Project

### 1. Language Set:
We are going to begin by deciding the specific set of languages that the workers will be asked to pronounce. This decision is going to be based on multiple factors. First, we need to determine what languages are feasible for MTurk workers, based on the languages that the MTurk workers speak. We are also going to make sure that we have a wide range of origins for the languages we choose, because if all of the languages are too similar the CNN model will have more difficulty differentiating them. *(1 point)*

### 2. Dictionary:
Collect a dictionary of words we want the workers to pronounce. This dictionary will be approximately 1000 words per language (this will depend on how much funding can be secured). The words are going to be provided by a dictionary of multiple languages. We will aim to pick the most common words in each language if we can find resources to do that for each language. *(1 point)*

### 3. HITS:
Make different "types"of HITS that include a particular set of words, as well as its own particular set of 5 control words. The control words come from annotated audio data (ex. We have french audio data for which we know what word it is and that it is in French). We will specify on the HIT that there should be no background noise when recording. *(2 points)*

### 4. Data Collection:
Collect the data - have multiple workers answer the same HIT, and filter which workers can complete the task based on what language they self-identify as speaking. We assume that we want a large baseline of hits for each word so that the classifier can learn about the pronunciation of each word from many recordings. *(2 points)*

### 5. Audio Conversion:
Convert audio data to spectrograms with matlab through the function plt.specgram. The audio recordings can be downloaded as mp3 or wav files, and converting them to spectrograms will be a relatively easy step.  This is necessary though because it is easier for classifiers to look at spectrograms than classify audio. *(1 point)*

### 6. Quality control:
The control words are real words that we know are pronounced a particular way for a language (we’ll have the audio files of the correct pronunciation, which we will convert to spectrograms) and we measure how similar the two spectrograms are and decide on an appropriate threshold to keep or eliminate data. *(3 points)*

### 7. Aggregation
In the aggregation step, we are going to use the quality rankings of each worker to weight the hit audio responses by how well the spectrogram of their control audio matches up to the ground truth spectrogram. Transforming the spectrogram into the  Fourier domain and gathering the top 5 spatio-temporal frequencies and finding the difference of these values for two spectrograms. Intuitively, the word “food” would have a very stable spectrogram whereas  “caterpillar” would have a very wavey one and so they would have different frequencies in the spatio-temporal domain. We can also use sound-frequency measure from the audio-file as an additional difference estimator. If a file/image has low difference with the mean then we know that it is a good data point. *(4 points)*

### 8. CNN model in Pytorch:
This model will be composed of grey-scale images. In order to keep the size of the input grey-scale images constant, we will take the audio of all the words of the same language and concatenate them together, make one giant long spectrogram, and divide that spectrogram evenly such that all the images are equal in size. After a few convolutional layers, there will be a fully connected layer whose activation function will classify which of the languages this language belongs to. *(4 points)*

**Total points: 18**

## Updates to README for Deliverable 2:

### Changes Made
After reviewing our steps and the time allotted to complete the project, we decided to make several changes. First, we are going to eliminate the machine learning aspect of this project, as we want to focus on getting accurate data and creating a strong database rather than stretching ourselves too thin in terms of how much time we have. As a result of this change, we are now going to have three passes. 

Our first pass is going to involve demographics and data collection. We will ask what language the worker speaks, their gender, and native languages. Then, we are going to have them record themselves using vocaroo.com pronouncing single words in their native languages.

Our second pass focuses on checking if the sound recording is good through other workers. We want workers to listen to audio clips, and specify whether they believe the HIT was good quality.

Our third pass will have workers rate audio recordings as “good” or “bad” based on if the pronunciations are correct in the audio recordings.

### QC
For our quality control method, we chose to determine which workers were best and use only the data from those selected workers.  For pass one, there are two control answers that must match for the worker to be considered “good” and for his/her results to be counted.  The first control is that there will be five sentences written out in 5 different languages, and the turker will need to select the one in the language that is appropriate for that HIT.  The second control is that there will be a phrase in the appropriate language that has its words scrambled, and the turker must select the combination that makes the most sense.  For example, “like I dogs”, “dogs like I”, “like dogs I”, and “I like dogs” would clearly be “I like dogs.”

For the second pass there is one control, in which the turkers will say if an audio recording is “good” or “bad” quality, and their answer must match our rating.  Our rating is based on if there is a lot of background noise or if the sound is clear and loud enough.

For the third pass, there will be one control.  Turkers will listen to an audio clip of one word, and type out how they believe it is pronounced.  For example, a clip saying “taxi” will accept answers of: “taxi, taksi, taksee, tacksee”.

### Aggregation
For aggregation, we want to make sure we can keep track of each worker that completes our HITs. As a result, we are going to create a file called ‘aggregation_output.csv’ that contains all of the information on the workers. This will include the workerId, which is unique to the worker, and demographics about the worker. When we are running our data and analyzing, this will make it easier to identify the chosen and native languages of each worker. 

### Raw Data
The raw data is the dictionary of words that we would like to be pronounced by the turkers in pass one. This is available in the bilingual dictionary provided to us by our professor. It is titled ‘dictionaries.tar.gz’. 

### Sample Input for QC
The three sample inputs are nets213DummyDataFinalCSV1.csv, nets213DummyDataFinalCSV2.csv, and nets213DummyDataFinalCSV3.csv.

### Sample Output for QC
Pass one outputs vocaroo.com urls.  Pass two outputs vocaroo.com urls.  Pass three outputs strings.  The sample is in QC_output_Aggregation_input.txt.

### Sample Input for Aggregation
Pass one outputs vocaroo.com urls.  Pass two outputs vocaroo.com urls.  Pass three outputs strings.  The sample is in QC_output_Aggregation_input.txt.

### Sample Output for Aggregation
The output of the aggregation, which is titled ‘Aggregation_Output.csv’ is going to contain the demographics of the workers: WorkerId, chosen_language, gender, and native_language. 

## Updates to README for Deliverable 3:

### Click on : 

- Depending on which language you can speak (english,french,spanish) you will click on a different HIT. The name of the HIT's language will be in the title. This process is 2-part. First you will do a HIT that is a qualification HIT - to make sure you really  speak the language that you say you do. Note that you have to click "accept" on the error that the links initially display. 
- English: https://workersandbox.mturk.com/projects/3PR0UJAG0Q0UM887TMZJP6XK1GTHJA/tasks/3M93N4X8HK6I7HNCMA08J2IZ37WSJ7?assignment_id=31IBVUNM9TILGRGDNHJT3B6VFEJFVX&auto_accept=true
- After clicking on the HIT you will be taken to a qualification test page that will ask you a few questions to make sure that you do in fact speak the language.
- If you passed the test,you will  be assigned the qualification. Once and if you are assigned the qualification you won't need to ever take the test again - no matter how many times you would like to redo the HIT for that language. If you fail though, you will no longer be able to try the qualification test for that language. 
- After you received the qualification, you will be able to accept the  HIT for the real qualification-test for that language. Note that you have to click "accept" on the error that the links initially display. 
- English: https://workersandbox.mturk.com/projects/38FT9G80EMR0HYW7W7BW5LAC55YHLC/tasks/3J6BHNX0U9BG2O1PWZJYLN86VXOKNM?assignment_id=3E7TUJ2EGD5QL0PETAJ7NTEDC9K9D0&auto_accept=true
- All HITs can be found at: https://workersandbox.mturk.com/requesters/A2C1UPBEGUY9Y6/projects

- ALSO NOTE: Passes 2 and 3 are set up in Mturk Sandbox but are not published yet because they need to be run with data collected from Pass 1

### Analysis Planned

- Our final product will be the data collected.  However, we will do some simple analysis of the data by graphing correct pronunciations of words by gender and native language.