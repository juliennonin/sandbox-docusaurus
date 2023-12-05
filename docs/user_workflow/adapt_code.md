# Adapt your code 

You have an existing function executing locally or on a docker for example, you would like to execute it on the Craft AI platform.

Whether it be a very basic function, one with inputs and/or outputs, or one that uses external data, it may be necessary to adapt the code to make it runnable without error on the platform.

```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">
<strong>💡 Best practice, have code ready for production</strong>

<ol>
    <li>
        Functional application design:
        <ul>
            <li>Structure your production code into nested functions to promote modularity, reuse, and I/O tracking.</li>
            <li>Do not use notebooks for production; use Python scripts and associated functions.</li>
            <li>Identify the main inputs and desired outputs for the main function.</li>
        </ul>
    </li>

    <li>
        Application evolution management:
        <ul>
            <li>Version your code using Git to monitor development and track changes throughout the application's lifecycle.</li>
            <li>Commit and push your code when you're ready to release it.</li>
        </ul>
    </li>

    <li>
        Explicit dependencies for stability:
        <ul>
            <li>Choose and declare the right dependencies in requirements.txt to ensure constant functionality.</li>
            <li>Specify the version of Python compatible with your project during commissioning (available directly in the platform, project parameter).</li>
        </ul>
    </li>
</ol>
</div>
```

## Prerequisites

Before using the Craft AI platform, make sure you have completed the following prerequisites:

1. **Get access to an environment**
2. **Connect the SDK**
    
    If this is not the case, you can go to this page for more information : [Connect to the platform](https://www.notion.so/Connect-to-the-platform-a931190b000d444d971a96c3423d9d20?pvs=21) 
    

## How I Encapsulate a basic script ?

Before explaining why encapsulate, let's first look at what encapsulation is in the Craft AI platform. Encapsulation is the act of taking your python code and putting it into a standard object for the platform that allows it to run with all the specific features it needs.

For example, encapsulation allows you to :

- Have all pip libraries correctly installed
- Receive and send data with the platform and your users
- Etc.

Your script encapsulated in the platform is called a “step”.

The aim of the platform is to enable you to create a step from your code with as little change as possible to your source code. Some adaptations may therefore be necessary, and we'll explain them here.

### Encapsulate “Hello world” case

The platform encapsulates Python scripts in order to execute them. For reasons of ease of use (particularly with regard to input/output), the platform encapsulates Python functions directly.

Let's imagine a `hello_world.py` script:

❌ this script does not work

```python
print ("Hello world)
```

✅ this script works

```python
def fct_hello(): 
	print ("Hello world)
```

Once you have uploaded your script to the repository linked to your environment. You can use the Python SDK to request encapsulation of your script with just 1 line of code:

```python
sdk.create_step(
    function_path="hello_world.py", # Path of were is the script file in your repo
    function_name="fct_hello", # Name of function to run
    step_name="step_name" # Unique name to identify your step in your environment
)
```

Finally, when your step is ready, you can create a pipeline from it that will be ready to be executed at any time by the platform.

### Encapsulate script who need to pip install libraries

In data science projects, it is common to use libraries not native to Python in our code (generally installed with pip). As part of the encapsulation process, this must also be specified when the step is created using a requirement.txt file.

To do this, add the requiremlent.txt file to the repository where the script to be executed in the pipeline is located, then specify it when the step is created.

```python
sdk.create_step(
	function_path="hello_world.py", # Path of were is the script file in your repo
	function_name="fct_hello", # Name of function to run
	step_name="step_name" # Unique name to identify your step in your environment

	# arg requirements_path should be in dict in container_config parameter
	container_config = { 
		"requirements_path": "requirements.txt" 	# requirement path in repository
	},
)
```


```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">

ℹ️ In addition to pip dependencies, you can add Linux-compatible system dependencies (equivalent to an <code class="docutils literal notranslate"><span class='pre'>apt-get install</span></code>).
Note that this is cumulative with pip dependencies.<br/><br/>

Example:<br/>

```

```python
sdk.create_step(
	function_path="hello_world.py", # Path of were is the script file in your repo
	function_name="fct_hello", # Name of function to run
	step_name="step_name" # Unique name to identify your step in your environment

	# arg requirements_path should be in dict in container_config parameter
	container_config = { 
		"system_dependencies": ["python3-opencv", "python3-scipy"]# list of dependancy name
	},
)
```

```{raw} html
</div>
```

### Encapsulate a script who use other existing functions of my repository

By default, the folders/files selected are copied from the repository to the step. The default selection is defined in the project parameters. If necessary, this can be changed to include other files from the repository or, on the contrary, to deselect them. The 2 conditions are :

- The python script must be part of the selected folders
- The content of all the selected folders must be less than 5MB.

Example: 

```python
sdk.create_step(
	function_path="hello_world.py", # Path of were is the script file in your repo
	function_name="fct_hello", # Name of function to run
	step_name="step_name" # Unique name to identify your step in your environment

	container_config = { 
		# import folder "/src"  and file "asset/data.csv" from repo to step
		"included_folders": ["src", "asset/data.csv"] 
	},
)
```

## How I Encapsulate a script with input and output ?

When I encapsulate the function in my script, it can request values as input parameters and return values as output with `return`. How do I interact between these elements and the platform?

To do this, we use the Input and Output system. These are elements that allow us to:

- Transmit data from the platform to the function parameters using **Inputs**.
- Transmit the data returned by the function to the platform using **Outputs**.

Note that the inputs and outputs of a step are defined when it is created (see example below).

```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">

ℹ️ To tell the platform where to fetch data for inputs and where to send data for outputs, we use mappings that we define when we deploy the pipeline. For more information, click here.

</div>
```

### Which data types are available ?

Here is a list of possible types for inputs and outputs:

- array
- boolean
- json
- number
- string
- file

Note that the input and output system automatically converts data into objects that can be used in Python. For example, JSON become Python dict, arrays become Python lists, etc.

```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">
```

ℹ️ The files work a little differently, and if you need to access data from external Data Sources, more information **[here](./access_data)**.

```{raw} html
</div><br/>
```

**Example :** 

In this example, we define two inputs of type number and JSON and an output of type array. The step can be represented as follows:

```{image} ./../screen/step_schema_workflow.png
:width: 800
```

```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">

ℹ️ In this diagram, the arrows with "Adapt process" represent the automatic conversion of types by the platform mentioned earlier.

</div>
```

Our source code, which will be contained in a function with two parameters and which returns a list in its `return`. Here is an example of python code in a [`script.py`](http://script.py/) file:

```python
def my_function(int_value, dictionary):
    # Print the parameters
    print("Parameter int:", int_value)
    print("Parameter dict:", dictionary)

    # Create the array (list) using the values from the dictionary
    result = list(dictionary.values())
    result.append(int_value)

    # Return the resulting array
    return result
```

Once the [`script.py`](http://script.py/) file has been sent to the repository, you can run the python code that uses the Craft AI SDK to create the inputs, outputs, and step:

```python
# Import and init craft AI SDK before 

step_input1 = Input(
  name="int_value", # same name as 1er parameter mandatory
	data_type="number",
)

step_input2 = Input(
  name="dictionary",# same name as 2nd parameter mandatory
	data_type="json",
)

step_output = Output(
  name="result",
	data_type="array"
)

sdk.create_step(
    function_path="script.py",
    function_name="my_function", 
    step_name="step_A",
    inputs=[step_input1, step_input2],
    outputs=[step_output]
)
```

```{warning}
Beware, for now all existing data types are not available yet (for example pd.DataFrame, pd.Series, etc.). You have to make sure you adapt your function’s code to be compatible.

To do so, you can pick among many various IO types already available.

```

### How to have a default input value ?

In order for certain step code to function correctly, it is possible that certain input values are mandatory in order to launch execution. There are 2 solutions for this:

- `is_required`: Used to make the input value mandatory in order to launch execution. If this is the case, execution will return an error without executing the code.
- `default_value`: Used to give a default value to the input when the basic value used is empty.

```{raw} html
<div style="background-color:#f3f6f6; padding: 12px;">

ℹ️ If the value of an input is required and has a default value, then the default value will be used for execution in the event of a missing value.

</div>
```

**Example :** 

For this example, we'll use the source code of the step we defined in the previous example. However, we're going to modify the code calling the Craft AI platform to notify it :

- A default value for `int_value`.
- That the `dictionary` input is mandatory for executing the step

```python
# Import and init craft AI SDK before 

step_input1 = Input(
  name="int_value", # same name as 1er parameter mandatory
	data_type="number",
	default_value=12,
)

step_input2 = Input(
  name="dictionary",# same name as 2nd parameter mandatory
	data_type="json",
	is_required=True,
)

step_output = Output(
  name="result",
	data_type="array"
)

sdk.create_step(
    function_path="script.py",
    function_name="my_function", 
    step_name="step_A",
    inputs=[step_input1, step_input2],
    outputs=[step_output]
)
```

## Full example with a script how used Docker

In this example, we will adapt an ML application (image classification) with :

- Python dependencies
- System dependencies
- Two string inputs (the access path to the image and the model in the data store)
- One string output (the classification result)

Python application source code :

```python
import cv2
import numpy as np
from tensorflow.keras.models import load_model

def perform_inference(image_path, model_path):
    # Load the pre-trained model
    model = load_model(model_path)

    # Read the image using OpenCV
    image = cv2.imread(image_path)

    # Preprocess the image (you may need to adjust this based on your model requirements)
    # Example: Resize the image to the input size expected by the model
    input_size = (224, 224)
    preprocessed_image = cv2.resize(image, input_size)
    preprocessed_image = preprocessed_image / 255.0  # Normalize pixel values to [0, 1]

    # Perform inference using the loaded model
    prediction = model.predict(np.expand_dims(preprocessed_image, axis=0))

    # Replace this with your post-processing logic based on the model output
    # For example, if it's a classification model, you might want to get the class with the highest probability
    predicted_class = np.argmax(prediction)

    return predicted_class

# Example usage
image_path = 'path/to/your/image.jpg'
model_path = 'path/to/your/model.h5'
result = perform_inference(image_path, model_path)

print(f"Predicted Class: {result}")
```

Requirements.txt : 

```
numpy
tensorflow
```

If you want to be able to run this script locally, you could imagine this script (bash) being run upstream:

- Bash command
    
    ```bash
    # Install OpenCV using apt-get
    # Note: This assumes you are using a Debian-based system
    sudo apt-get update
    sudo apt-get install -y python3-opencv
    
    # Upgrade pip and install Python dependencies from requirements.txt
    pip install --upgrade pip
    pip install -r requirements.txt
    
    # Run app.py
    python app.py
    ```
    

Or its equivalent with a dockerfile :

- Dokerfile
    
    ```docker
    # Use an official Python image as a parent image
    FROM python:3.9-slim
    
    # Set the working directory to /app
    WORKDIR /app
    
    # Copy the current directory contents into the container at /app
    COPY . /app
    
    # Install OpenCV using apt-get
    RUN apt-get update && apt-get install -y \
        python3-opencv
    
    # Install any Python dependencies from requirements.txt
    RUN pip install --upgrade pip && \
        pip install -r requirements.txt
    
    # Make port 80 available to the world outside this container
    EXPOSE 80
    
    # Run app.py when the container launches
    CMD ["python", "app.py"]
    ```
    

Once the script `app.py` and the `requirements.txt` file are on the repository, all you have to do is use the Craft AI SDK to create the inputs and output, then create the step with the correct parameters.

```python
# Import and init craft AI SDK before 

step_input1 = Input(
  name="image_path", 
	data_type="string",
	is_required=True,
)

step_input2 = Input(
  name="model_path",
	data_type="string",
	is_required=True,
)

step_output = Output(
  name="result",
	data_type="string"
)

sdk.create_step(
  function_path="app.py",
  function_name="perform_inference", 
  step_name="step_B",
	container_config = { 
    "requirements_path": "requirements.txt"
    "system_dependencies": ["python3-opencv"]
  },
  inputs=[step_input1, step_input2],
  outputs=[step_output]
)
```

The values given to the Python script when the function is called (see code below) will be given at each execution, and can therefore be modified by the user calling the step. More details [**here**](./run_serve_pipeline).