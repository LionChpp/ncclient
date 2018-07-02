[![Build Status](https://travis-ci.org/ncclient/ncclient.svg?branch=master)](https://travis-ci.org/ncclient/ncclient)
[![Coverage Status](https://coveralls.io/repos/github/ncclient/ncclient/badge.svg?branch=master)](https://coveralls.io/github/ncclient/ncclient?branch=master)
[![Documentation Status](https://readthedocs.org/projects/ncclient/badge/?version=latest)](https://readthedocs.org/projects/ncclient/?badge=latest)

ncclient: Python library for NETCONF clients
--------------------------------------------


ncclient is a Python library that facilitates client-side scripting
and application development around the NETCONF protocol. `ncclient` was
developed by [Shikar Bhushan](http://schmizz.net). It is now maintained
by [Leonidas Poulopoulos (@leopoul)](http://ncclient.org)

**Docs**: [http://ncclient.readthedocs.org](http://ncclient.readthedocs.org)

**PyPI**: [https://pypi.python.org/pypi/ncclient](https://pypi.python.org/pypi/ncclient)

#### Requirements:
* Python 2.7 or Python 3.4 to 3.6
    * Python 3.7 excluded due to use of `async` keyword for versions `0.5.4` and earlier
* setuptools 0.6+
* Paramiko 1.7+
* lxml 3.3.0+
* libxml2
* libxslt

If you are on Debian/Ubuntu install the following libs (via aptitude or apt-get):
* libxml2-dev
* libxslt1-dev

#### Installation:

    [ncclient] $ sudo python setup.py install
    
or via pip:

    pip install ncclient

#### Examples:

    [ncclient] $ python examples/juniper/*.py

### Usage
#### Get device running config
Use either an interactive Python console (ipython)
or integrate the following in your code:

    from ncclient import manager

    with manager.connect(host=host, port=830, username=user, hostkey_verify=False) as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

As of 0.4.1 ncclient integrates Juniper's and Cisco's forks, lots of new concepts
have been introduced that ease management of Juniper and Cisco devices respectively.
The biggest change is the introduction of device handlers in connection paramms.
For example to invoke Juniper's functions annd params one has to re-write the above with ***device_params={'name':'junos'}***:

    from ncclient import manager

    with manager.connect(host=host, port=830, username=user, hostkey_verify=False, device_params={'name':'junos'}) as m:
        c = m.get_config(source='running').data_xml
        with open("%s.xml" % host, 'w') as f:
            f.write(c)

Device handlers are easy to implement and prove to be futureproof.

#### Supported device handlers

* Juniper: device_params={'name':'junos'}
* Cisco CSR: device_params={'name':'csr'}
* Cisco Nexus: device_params={'name':'nexus'}
* Cisco IOS XR: device_params={'name':'iosxr'}
* Cisco IOS XE: device_params={'name':'iosxe'}
* Huawei: device_params={'name':'huawei'}
* Alcatel Lucent: device_params={'name':'alu'}
* H3C: device_params={'name':'h3c'}
* HP Comware: device_params={'name':'hpcomware'}
* Server or anything not in above: device_params={'name':'default'}


### Changes | brief - v0.5.3

* Add notifications support
* Add support for ecdsa keys
* Various bug fixes

### Contributors

* v0.5.4: @adamcubel, Joel Teichroeb, @leopoul, Chase Garner, @budhadityabanerjee, @earies, @ganeshrn, @vnitinv, Siming Yuan, @mirceaaulinic, @stacywsmith, Xavier Hardy, @jwwilcox, @QijunPan, @avangel, @marekgr, @hugovk, @felixonmars, @dexteradeus
* v0.5.3: [Justin Wilcox](https://github.com/jwwilcox), [Stacy W. Smith](https://github.com/stacywsmith), [Mircea Ulinic](https://github.com/mirceaulinic), [Ebben Aries](https://github.com/earies), [Einar Nilsen-Nygaard](https://github.com/einarnn), [QijunPan](https://github.com/QijunPan)
* v0.5.2: [Nitin Kumar](https://github.com/vnitinv), [Kristian Larsson](https://github.com/plajjan), [palashgupta](https://github.com/palashgupta), [Jonathan Provost](https://github.com/JoProvost), [Jainpriyal](https://github.com/Jainpriyal), [sharang](https://github.com/sharang), [pseguel](https://github.com/pseguel), [nnakamot](https://github.com/nnakamot), [Алексей Пастухов](https://github.com/p-alik), [Christian Giese](https://github.com/GIC-de), [Peipei Guo](https://github.com/peipeiguo), [Time Warner Cable Openstack Team](https://github.com/twc-openstack)
* v0.4.7: [Einar Nilsen-Nygaard](https://github.com/einarnn), [Vaibhav Bajpai](https://github.com/vbajpai), Norio Nakamoto 
* v0.4.6: [Nitin Kumar](https://github.com/vnitinv), [Carl Moberg](https://github.com/cmoberg), [Stavros Kroustouris](https://github.com/kroustou) 
* v0.4.5: [Sebastian Wiesinger](https://github.com/sebastianw), [Vincent Bernat](https://github.com/vincentbernat), [Matthew Stone](https://github.com/bigmstone), [Nitin Kumar](https://github.com/vnitinv)
* v0.4.3: [Jeremy Schulman](https://github.com/jeremyschulman), [Ray Solomon](https://github.com/rsolomo), [Rick Sherman](https://github.com/shermdog), [subhak186](https://github.com/subhak186)
* v0.4.2: [katharh](https://github.com/katharh), [Francis Luong (Franco)](https://github.com/francisluong), [Vincent Bernat](https://github.com/vincentbernat), [Juergen Brendel](https://github.com/juergenbrendel), [Quentin Loos](https://github.com/Kent1), [Ray Solomon](https://github.com/rsolomo), [Sebastian Wiesinger](https://github.com/sebastianw), [Ebben Aries](https://github.com/earies) 
* v0.4.1: [Jeremy Schulman](https://github.com/jeremyschulman), [Ebben Aries](https://github.com/earies), Juergen Brendel

