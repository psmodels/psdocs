Transforms
==========

Park Transform
--------------

abc to dq
'''''''''

.. code-block:: matlab

   T_p = 2.0/3.0*[[ cos(theta), cos(theta-2.0/3.0*pi), cos(theta+2.0/3.0*pi)],
                  [-sin(theta),-sin(theta-2.0/3.0*pi),-sin(theta+2.0/3.0*pi)]];


dq to abc
'''''''''

.. code-block:: matlab

    T_p_inv = [[            cos(theta),            -sin(theta)],
               [ cos(theta-2.0/3.0*pi), -sin(theta-2.0/3.0*pi)],
               [ cos(theta+2.0/3.0*pi), -sin(theta+2.0/3.0*pi)]];


abc to dqz
''''''''''

.. code-block:: matlab

   T_p = 2.0/3.0*[[ cos(theta), cos(theta-2.0/3.0*pi), cos(theta+2.0/3.0*pi)],
                  [-sin(theta),-sin(theta-2.0/3.0*pi),-sin(theta+2.0/3.0*pi)],
                  [        0.5,                   0.5,                   0.5]];
                  

dqz to abc
''''''''''

.. code-block:: matlab

    T_p_inv = [[            cos(theta),            -sin(theta), 1.0],
               [ cos(theta-2.0/3.0*pi), -sin(theta-2.0/3.0*pi), 1.0],
               [ cos(theta+2.0/3.0*pi), -sin(theta+2.0/3.0*pi), 1.0]];


Transforms Power Invariant Forms
================================

Park Transform
--------------

abc to dqz
''''''''''

.. code-block:: matlab

   T_p = sqrt(2.0/3.0)*[[   cos(theta), cos(theta-2.0/3.0*pi), cos(theta+2.0/3.0*pi)],
                        [  -sin(theta),-sin(theta-2.0/3.0*pi),-sin(theta+2.0/3.0*pi)],
                        [sqrt(2.0)/2.0,         sqrt(2.0)/2.0,         sqrt(2.0)/2.0]];


dqz to abc
''''''''''

.. code-block:: matlab

    T_p_inv = T_p.';
