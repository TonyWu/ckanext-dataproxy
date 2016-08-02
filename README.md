# ckanext-dataproxy
ckanext-dataproxy is [CKAN](https://github.com/ckan/ckan) extension that enables previewing data from remote databases via SQLAlchemy. The extension is compatible with datastore by masking the dataproxy resource as a datastore resource so it could be requested via `/api/3/action/datastore_search` or previewed in-browser with recline-preview.


Usage:

- [CKAN 2.2.x](https://github.com/cphsolutionslab/ckanext-dataproxy/wiki/Usage-with-CKAN-2.2.x)
- [CKAN 2.5.x](https://github.com/cphsolutionslab/ckanext-dataproxy/wiki/Usage-with-CKAN-2.5.x)

## Installation 
__NB! This module is developed for CKAN v2.2.x and v2.5.x, compatibility with other versions is not ensured__

1) Clone this repo  

```sh
cd /usr/lib/ckan/default/src
git clone https://github.com/cphsolutionslab/ckanext-dataproxy.git
cd ckanext-dataproxy
```

 2) Install requirements (It is not required to install drivers for databases you don't plan to proxy, see the file)  
```
pip install -r requirements.txt
```

__Additional packages may be required to compile the database-specific drivers. For Ubuntu, you may need:__

```
sudo apt-get install build-essential libmysqlclient-dev freetds-dev
```

3) Install the plugin  

```sh
python setup.py develop
```

4) Set the dataproxy secret in your CKAN settings file (e.g. /etc/ckan/default/production.ini)

For example, in the settings file:

```sh
# Password for AES256 key generation
ckan.dataproxy.secret = c9f56fdfd12ee615f3d858... # Don't actually use this string, use a random secret.
```
You can run the following command in your shell to generate a random secret:
```sh
echo "import hashlib ; from uuid import uuid4 ; print hashlib.sha256(str(uuid4())).hexdigest()" | python -
```


## Enable on CKAN 2.2.x

Enable the extension by appending `dataproxy` to `ckan.plugins` variable in your configuration file:

```
ckan.plugins = stats text_preview ... dataproxy
```


## Enable on CKAN 2.5.x

Enable the extension by appending `dataproxy` and `dataproxy_view` to `ckan.plugins` variable in your configuration file:

```
ckan.plugins = stats text_preview ... dataproxy dataproxy_view
```

Then append `dataproxy_view` to `ckan.views.default_views` variable:

```
ckan.views.default_views = image_view ... dataproxy_view
```
