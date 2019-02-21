Transforms
==========

Park Transform
--------------

abc to dq
'''''''''

.. code-block:: matlab

   T_p = 2.0/3.0*[[ cos(theta), cos(theta-2.0/3.0*pi), cos(theta+2.0/3.0*pi)],
                  [-sin(theta),-sin(theta-2.0/3.0*pi),-sin(theta+2.0/3.0*pi)]]


dq to abc
'''''''''

.. code-block:: matlab

    T_p_inv = [[          cos(theta),              -sin(theta)],
               [ cos(theta-2.0/3.0*pi), -sin(theta-2.0/3.0*pi)],
               [ cos(theta+2.0/3.0*pi), -sin(theta+2.0/3.0*pi)]]

