**********
pypi-stats
**********

..
    .. image:: https://img.shields.io/pypi/l/pypi-stats.svg
               :target: https://opensource.org/licenses/MIT
               :alt: License
    .. image:: https://img.shields.io/badge/github-repo-yellow.jpg
               :target: https://github.com/fmenabe/pypi-stats
               :alt: Code repo

Simple tool that shows PyPI downloads of packages by retrieving data from `Google
BigQuery <https://cloud.google.com/bigquery/>`_ and the ``[the-psf:pypi.downloads]``
public dataset.


Creating a service account for using BigQuery
=============================================

This is probably the hardest part!

You need to:

    1) Go to the `Google API console <https://console.developers.google.com/apis/>`_
    2) Go to credentials and create new credentials. If you don't already have a project,
       you will be asked to create one (the name of the project is not really important)
    3) Create a **Service Account key** with the *BigQuery Job User* role (again the name
       is not really important). It will ask you to download the JSON file you need to
       authenticate to BigQuery.

**Note: Take care that free usage of BigQuery is limited and it is easy to exceed quota!**


Installation
============

.. code::

    pip install pypi-stats


Examples
========

**Downloads since the start of the month:**:

.. code::

    pypi-stats -t TOKENPATH.json yamlordereddictloader clg
    ┌───────────────────────┬─────────┬─────┬──────┬───────┐
    │ Name                  │ Version │ Day │ Week │ Month │
    ├───────────────────────┼─────────┼─────┼──────┼───────┤
    │ clg                   │ 2.0.0   │ 2   │ 37   │ 37    │
    │ clg                   │ *       │ 2   │ 37   │ 37    │
    ├───────────────────────┼─────────┼─────┼──────┼───────┤
    │ yamlordereddictloader │ 0.4.0   │ 42  │ 399  │ 399   │
    │ yamlordereddictloader │ 0.3.0   │ -   │ 24   │ 24    │
    │ yamlordereddictloader │ 0.2.2   │ 1   │ 12   │ 12    │
    │ yamlordereddictloader │ 0.1.1   │ -   │ 31   │ 31    │
    │ yamlordereddictloader │ 0.1.0   │ -   │ 14   │ 14    │
    │ yamlordereddictloader │ *       │ 43  │ 480  │ 480   │
    └───────────────────────┴─────────┴─────┴──────┴───────┘

**Downloads since the start of the year:**

.. code::

    pypi-stats -t TOKENPATH.json --year clg
    ┌───────────────────────┬─────────┬─────┬──────┬───────┬──────┐
    │ Name                  │ Version │ Day │ Week │ Month │ Year │
    ├───────────────────────┼─────────┼─────┼──────┼───────┼──────┤
    │ clg                   │ 2.3.1   │ -   │ 3    │ -     │ 14   │
    │ clg                   │ 2.3.0   │ -   │ -    │ -     │ 8    │
    │ clg                   │ 2.0.0   │ 2   │ 77   │ 37    │ 537  │
    │ clg                   │ *       │ 2   │ 80   │ 37    │ 559  │
    └───────────────────────┴─────────┴─────┴──────┴───────┴──────┘

**Save statistics in a JSON file:**

.. code::

    pypi-stats -t TOKENPATH.json --format json --output-file stats.json yamlordereddictloader clg

**Re-use the JSON file to show statistics:**

.. code::

    pypi-stats --file stats.json
    ┌───────────────────────┬─────────┬─────┬──────┬───────┐
    │ Name                  │ Version │ Day │ Week │ Month │
    ├───────────────────────┼─────────┼─────┼──────┼───────┤
    │ clg                   │ 2.0.0   │ 2   │ 37   │ 37    │
    │ clg                   │ *       │ 2   │ 37   │ 37    │
    └───────────────────────┴─────────┴─────┴──────┴───────┘
