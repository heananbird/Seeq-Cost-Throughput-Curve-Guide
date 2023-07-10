Calculation Metric
==================

There are 8 calculated metrics that are derived from 12 tag signals. The original 12 tag signals are:

- Feeder_1_PV
- Feeder_2_PV
- Feeder_3_PV
- Feeder_4_PV
- Feeder_5_PV
- Feeder_6_PV
- Feeder_7_PV
- Conveyor_Speed_PV
- Product_Manufactured
- Vacuum

Each of the tags was pulled from each line and separate calculations were performed to get the following metrics:

- Downtime: Periods of time in which no material is flowing AND Conveyor is not running

Seeq Formula
------------

.. code-block:: console

   '(($f1.resample(5min).replaceNotValid(0)+$f2.resample(5min).replaceNotValid(0)+$f3.resample(5min).replaceNotValid(0)+$f4.resample(5min).replaceNotValid(0)+$f5.resample(5min).replaceNotValid(0)+$f6.resample(5min).replaceNotValid(0)+$f7.resample(5min).replaceNotValid(0)+$ba1.resample(5min).replaceNotValid(0)+$ba2.resample(5min).replaceNotValid(0)+$ba3.resample(5min).replaceNotValid(0)) == 0).merge(0min).combineWith(($cs.resample(5min) == 0).merge(0min).removeShorterThan(30min))'

- Production Runs: Periods where not downtime is occurring AND Product_Manufactured signal identifies a product being made

Seeq Formula
------------

.. code-block:: console

   '(($pm.remove(isEqualTo("")).setMaxInterpolation(30minutes).resample(10min).toCondition("Production Properties").fragment(keepProperties()).keep("Production Properties", isNotEqualTo("")) - $d).merge(0min).shrink(20min).removeShorterThan(1.5hour)).removeLongerThan(312h)'

- Board Ft/Hour: For each production run a discrete value representing the average Conveyor_Speed for that production run.

Seeq Formula
------------

.. code-block:: console

   '$cs.resample(5min).setUnits("ft/min").convertUnits("ft/hr").aggregate(average(), $pr.removeLongerThan(312h), middleKey(), 0s)'

- Board Ft/Production Run: For each production run a discrete value representing the length of the production run multiplied by the Board Ft/Hour

Seeq Formula
------------

.. code-block:: console

   '$bfth*$pr.removeLongerThan(312h).aggregate(totalDuration("h"), $pr.removeLongerThan(312h), middleKey(), 0s)'

- Total Cost: A signal that represents a constant cost estimate for each feeder input added across all feeders.

Seeq Formula
------------

.. code-block:: console

   'A2+3'

- Total Cost/Production Run: A discrete value that is the integral of the costs for time periods across a given production run.

Seeq Formula
------------

.. code-block:: console

   '$tc.aggregate(totalized("h"), $pr.removeLongerThan(312h), middleKey(), 0s).setUnits("$")'

- Cost/Board Ft: A discrete value that represents the Total Cost/Production Run divided by the Board Ft/Production Run

Seeq Formula
------------

.. code-block:: console

   '$tcpr/$bftpr'

Asset Diagram:
--------------

.. image:: /path/to/your/image.png
   :alt: optional alt text
   :height: 300px
   :width: 200px
   :scale: 50
   :align: center

.. note::

   This is a test image.
