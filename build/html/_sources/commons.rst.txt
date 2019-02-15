Transforms
==========

Park Transform
--------------

abc 2 dq
''''''''

.. code-block:: matlab

   T_p = 2.0/3.0*[[ cos(theta), cos(theta-delta*pi), cos(theta+delta*pi)],
                  [-sin(theta),-sin(theta-delta*pi),-sin(theta+delta*pi)]]


dq 2 abc
''''''''

.. code-block:: matlab

    T_p_inv = [[          cos(theta),          -sin(theta)],
               [ cos(theta-delta*pi), -sin(theta-delta*pi)],
               [ cos(theta+delta*pi), -sin(theta+delta*pi)]]

