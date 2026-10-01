Dubai community rental yields: June 2026
=======================================

This guide documents the owned dataHabibi CSV snapshot for June 2026. It
explains the fields, shows the recorded values, and provides a reproducible
way to read the file. The snapshot contains twelve named Dubai communities
and one Dubai city-average row. It is a historical snapshot, not a live feed.

Source: `https://datahabibi.ae/ <https://datahabibi.ae/>`_

Download and provenance
-----------------------

:download:`Download the original CSV <dubai-community-yields-june-2026.csv>`.

The same dataset is published on
`data.gouv.fr <https://www.data.gouv.fr/datasets/dubai-community-rental-yields-june-2026-datahabibi>`_.
The CSV is reproduced here without changing its recorded values. This guide
is published by dataHabibi; it does not claim affiliation with a government,
university, or research institution.

Data dictionary
---------------

``Community``
    The community label recorded in the snapshot, or ``Dubai city average``.
``Gross rental yield percent``
    A percentage value recorded in the source snapshot. For example, 9.98
    means 9.98 percent, not the decimal fraction 9.98. The CSV does not
    contain the rents or prices required to independently recompute it.
``Buildings tracked``
    The count labelled Buildings tracked in the snapshot. Do not assume this
    is the denominator used to calculate yield.
``Yield sample size``
    The count labelled Yield sample size in the snapshot. It is blank for
    the city-average row. Blank means not supplied, not zero. The CSV does
    not specify the sample unit or aggregation method.
``Snapshot``
    The recorded period, June 2026, in every row.
``Source``
    The original source address, https://datahabibi.ae/, in every row.

Recorded values
---------------

.. csv-table:: June 2026 snapshot
   :file: dubai-community-yields-june-2026.csv
   :header-rows: 1
   :widths: 24, 16, 14, 14, 14, 18

Read the CSV with Python
------------------------

This example uses only Python's standard library. Save it next to the
CSV, or adjust the file path to its downloaded location.

.. code-block:: python

   import csv
   from decimal import Decimal

   with open("dubai-community-yields-june-2026.csv", newline="", encoding="utf-8") as source:
       rows = list(csv.DictReader(source))

   for row in rows:
       yield_percent = Decimal(row["Gross rental yield percent"])
       buildings = int(row["Buildings tracked"])
       sample_text = row["Yield sample size"]
       sample_size = int(sample_text) if sample_text else None
       print(row["Community"], yield_percent, buildings, sample_size)

Missing values and comparisons
------------------------------

Keep the city-average row separate when analysing community rows. Do not
replace its missing sample size with zero, and do not reconstruct its yield
by averaging the twelve displayed community yields: the CSV does not supply
the full city population, weights, or aggregation method.

Gross rental yield describes rental income relative to a property's price
before costs. It differs from net yield, total return, and a price forecast.
The snapshot does not include service charges, vacancy, maintenance,
financing, transaction costs, or a forecast. It cannot establish a property's
net return or guarantee future performance.

License and reuse
-----------------

The dataset and this documentation use
`Creative Commons Attribution 4.0 International (CC BY 4.0)
<https://creativecommons.org/licenses/by/4.0/>`_. Give attribution to
dataHabibi, identify the June 2026 snapshot, link to the license, and indicate
changes when distributing adaptations. The logo, brand assets and commercial
platform source code are outside this dataset/documentation release.

Contact
-------

For questions about the dataset documentation: Ibrahim Qorraj,
ibrahim@datahabibi.ae.
