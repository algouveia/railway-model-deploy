# Scikit model behind flask app on heroku

This is a very simplistic yet effective way to deploy a scikit binary
classifier behind a HTTP server on heroku.

There are 3 main topics to cover here

1. Serialization
    - This is covered in notebooks
1. Flask
    - Covered here in the readme
1. Deployment to heroku
    - Also covered here in the readme

### Before continuing

Topic #1 is the only one that is not covered here in this readme. It is covered in two notebooks
that you must read before moving on with the rest of this README.

[Notebook #1](https://github.com/LDSSA/heroku-example/blob/master/Train%20and%20Serialize.ipynb) has
to do with training and serializing a scikit model as well as how to prepare a new observation
that arrives for prediction.

[Notebook #2](https://github.com/LDSSA/heroku-example/blob/master/Deserialize%20and%20use.ipynb) has
to do with deserialization so that you can re-use a model on new observations without having to re-train
it.

## Flask

Have you already read and understood the notebooks on serialiation? Have you already tested your understanding
by pickling and un-pickling your scikit model? Yes yes? Alrighty then, you may continue on.

### What is flask

[Flask](http://flask.pocoo.org/) is an HTTP micro-framework. It is a very minimal code library that allows
for quick and simple HTTP server development and is a great alternative to bigger frameworks like Django.
However, be wary before moving forward with a big project using flask - it can get out of hand very quickly
without the enforced structure that other heavier frameworks like Django provide.

For us, since we only need a total of two endpoints and it doesn't even need to be RESTful, we can stick with
flask and be reasonably justified in it.

### First steps

In order to use flask, you will need to be writing some code in a regular
python file - no more notebooks here. The first step (assuming you have already
done `pip install flask` is to import it at the top of the file. Let's pretend
that we are working in a file called `app.py`

```py
TODO
```

### Making HTTP endpoints

With flask, creating an http endpoint is incredibly simple

## IMPORTANT NOTE

This repo is still in development! You may look for now but until I give the signal, it could change at any moment!

## Development

To run it locally, create a virtual environment

```
python3.6 -m venv ./venv
source venv/bin/activate
pip install -r requirements.txt
```

### Example observation

New observation comes in

```
 curl -X POST http://localhost:5000/predict -d '{"id": 0, "observation": {"Age": 22.0, "Cabin": null, "Embarked": "S", "Fare": 7.25, "Parch": 0, "Pclass": 3, "Sex": "male", "SibSp": 1}}' -H "Content-Type:application/json"
{
  "id": 1, 
  "observation_id": 0, 
  "predicted_class": true, 
  "proba": 0.09264179297127445, 
  "true_class": null
}
```

Get the true outcome

```
curl -X POST http://localhost:5000/update -d '{"id": 0, "true_class": 1}'  -H "Content-Type:application/json"
```

### Heroku utilities

Push new code after committing it

```
git push heroku master && heroku logs --tail
```

Restart the server

```
heroku ps:restart && heroku logs --tail
```
