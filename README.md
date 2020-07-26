#### This class shall be used to save the model after training and load the saved model for prediction.

```python
class FileOperation:
    
    def __init__(self):
        self.file_object = open('logs/fileOperationLogs.txt', 'a+')
        self.logger_object = AppLogger()
        self.model_directory = 'models/'
       
```

#### Save the model file to directory then entered the save_model method of the File_Operation class.create seperate directory for each cluster and remove previously existing models for each clusters then saving the model to file
   
   Description: Save the model file to directory
   Outcome: File gets saved
   On Failure: Raise Exception

```python
def save_model(self, model, filename):
    self.logger_object.log(self.file_object, 'Entered the save_model method of the File_Operation class')
        try:
            path = os.path.join(self.model_directory, filename)  # create seperate directory for each cluster
            if os.path.isdir(path):  # remove previously existing models for each clusters
                shutil.rmtree(self.model_directory)
                os.makedirs(path)
            else:
                os.makedirs(path)  #
            with open(path + '/' + filename + '.sav',
                      'wb') as f:
                pickle.dump(model, f)  # save the model to file
            self.logger_object.log(self.file_object,
                                   'Model File ' + filename + ' saved. Exited the save_model method of the Model_Finder class')

            return 'success'
        except Exception as e:
            self.logger_object.log(self.file_object,
                                   'Exception occured in save_model method of the Model_Finder class. Exception message:  ' + str(
                                       e))
            self.logger_object.log(self.file_object,
                                   'Model File ' + filename + ' could not be saved. Exited the save_model method of the Model_Finder class')
            raise Exception()
```
#### Entered the load_model method of the File_Operation class 

     Method Name: find_correct_model_file
     Description: Select the correct model based on cluster number
     Output: The Model file
     On Failure: Raise Exception
     
```python     
def find_correct_model_file(self, cluster_number):
self.logger_object.log(self.file_object,
                               'Entered the find_correct_model_file method of the File_Operation class')
        try:
            self.cluster_number = cluster_number
            self.folder_name = self.model_directory
            self.list_of_model_files = []
            self.list_of_files = os.listdir(self.folder_name)
            for self.file in self.list_of_files:
                try:
                    if (self.file.index(str(self.cluster_number)) != -1):
                        self.model_name = self.file
                except:
                    continue
            self.model_name = self.model_name.split('.')[0]
            self.logger_object.log(self.file_object,
                                   'Exited the find_correct_model_file method of the Model_Finder class.')
            return self.model_name
        except Exception as e:
            self.logger_object.log(self.file_object,
                                   'Exception occured in find_correct_model_file method of the Model_Finder class. Exception message:  ' + str(
                                       e))
            self.logger_object.log(self.file_object,
                                   'Exited the find_correct_model_file method of the Model_Finder class with Failure')
            raise Exception()
```

#Logger

## When you want to configure logging for your project, you should do it as soon as possible when the program starts. If app.logger is accessed before logging is configured, it will add a default handler. If possible, configure logging before creating the application object.
'''python
class AppLogger:
    def __init__(self):
        self.now = datetime.now()
        self.date = self.now.date()
        self.current_time = self.now.strftime("%H:%M:%S")

    def log(self, file_object, log_message):
        """This method will be used for logger all the information to the file."""

        file_object.write(
            str(self.date) + "/" + str(self.current_time) + "\t\t" + log_message + "\n")
'''















```
