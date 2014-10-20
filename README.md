# Map of Public Toilets in Australia 
*powered by Flask, Python, MongoDB, and Leaflet.js*

To deploy a clone of this application using the [`rhc` command line tool](http://rubygems.org/gems/rhc):

    rhc app create loofu python-2.7 mongodb-2.4 --from-code=https://github.com/codemiller/cloud-craft-python-au.git -s

To use Python 3.3 or 2.6, replace the Python cartridge version in the command.

Alternatively, [link to a web-based clone+deploy](https://openshift.redhat.com/app/console/application_type/custom?cartridges%5B%5D=python&scale=true&cartridges%5B%5D=mongodb-2&initial_git_url=https%3A%2F%2Fgithub.com%2Fcodemiller%2Fcloud-craft-python-au.git) on [OpenShift Online](http://OpenShift.com) or on [your own OpenShift cloud](http://openshift.github.io):

    https://openshift.redhat.com/app/console/application_type/custom?cartridges%5B%5D=python&scale=true&cartridges%5B%5D=mongodb-2&initial_git_url=https%3A%2F%2Fgithub.com%2Fcodemiller%2Fcloud-craft-python-au.git

A demo is available at: [http://loofu-cloudcraft.rhcloud.com/](http://loofu-cloudcraft.rhcloud.com/)

## Local Development

To run the application locally, install Python, MongoDB 2.4 or higher, and the required Python modules in _setup.py_ (these can be installed using [Pip](http://en.wikipedia.org/wiki/Pip_\(package_manager\)), eg: `sudo pip install Flask && sudo pip install pymongo`).

If you do not want to install MongoDB locally, you could instead use `rhc port-forward` and set the database connection parameters in _loofu.cfg_ to point to your instance of MongoDB hosted on OpenShift (or elsewhere).

Make sure MongoDB is running, and add the data and index with commands such as the following:

	mongoimport -d loofu -c toilets --type json --file data/NationalPublicToiletMap.json
	mongo loofu --eval 'db.toilets.ensureIndex( { "geometry.coordinates" : "2dsphere" } )'

Check that the default DB connection parameters in _loofu.cfg_ match your MongoDB instance.

Run the app on localhost with the following command:

    python app.py

## License and Credits
This code is dedicated to the public domain to the maximum extent permitted by applicable law, pursuant to CC0 (http://creativecommons.org/publicdomain/zero/1.0/)

App based on code by [TheSteve0](https://github.com/thesteve0/pythonwebmap) and [ryanj](https://github.com/ryanj/flask-base).

Toilet icons and banner contributed by [Ben Hoad](http://benhoad.net).
