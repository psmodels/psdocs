VSC 3-wire with L-Filter
========================


.. code-block:: matlab

     
    function [i_sd,i_sq,v_dc,dx] = vsc_l_dq(eta_d,eta_q,v_sd,v_sq,i_dc,omega,params,x)

    % parameters
    R_s = params(1);
    L_s = params(2);
    C_dc = params(3);

    % from the integrator to the states
    i_d  = x(1);
    i_q  = x(2);
    v_dc = x(3);
 
    % derivatives
    di_sd = 1/L_s*(eta_d*v_dc/2 + L_s*omega*i_sq - R_s*i_sd - v_sd);
    di_sq = 1/L_s*(eta_q*v_dc/2 - L_s*omega*i_sd - R_s*i_sq - v_sq);
    dv_dc = 1/C_dc*(0.5*(eta_d*i_sd + eta_q*i_sq - i_dc));
    
    % from derivatives to the integrator
    dx = [di_sd,di_sq,dv_dc];




Control CTRL1 VSC 3-wire L-filter
---------------------------------


.. code-block:: matlab

     
    function [eta_d,eta_q,dx] = ctrl_vsc(i_sd_ref,i_sq_ref,i_sd,i_sq,v_dc,omega,params,x)

    % parameters
    R_s = params(1);
    L_s = params(2);
    K_p = params(3);
    K_i = params(4);

    % from the integrator to the states
    xi_isd  = x(1);
    xi_is1  = x(2);
 
 
    % auxiliar
    e_isd =  i_sd_ref - i_sd;
    e_isq =  i_sq_ref - i_sq;
    

    % derivatives
    dxi_isd  = e_isd;
    dxi_isq  = e_isq;


    % auxiliar 
    u_d = K_p*e_isd + K_i*xi_isd;
    u_d = K_p*e_isq + K_i*xi_isq;


    % outputs
    eta_d  = 2 * v_dc * ( u_d  - L * omega * i_sq  + v_sd);
    eta_q  = 2 * v_dc * ( u_q  + L * omega * i_sd  + v_sq);

    % from derivatives to the integrator
    dx = [dxi_isd,dxi_isq];



