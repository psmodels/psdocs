(Doing) VSC 3-wire with LCL-Filter
==================================


.. code-block:: matlab

     
    function [i_sd,i_sq,v_dc,dx] = vsc_l_dq(v_sd,v_sq,omega,params,x)

    % parameters
    R_s = params(1);
    L_s = params(2);

    % from the integrator to the states
    i_d  = x(1);
    i_q  = x(2);
    v_dc = x(3);

 
    % derivatives
    di_d  = 1/L_s*(v_sd + L_s*omega*i_q - R_s*i_sd - v_sd);
    di_q  = 1/L_s*(v_sq - L_s*omega*i_d - R_s*i_sq - v_sq);
    dv_dc = 1/C_dc * ( 0.5 * (eta_d *i_sd  + eta_q * i_tq  - i_dc )
    
    % from derivatives to the integrator
    dx = [di_d,di_q,dv_dc];





