(Doing) VSC 3-wire with LCL-Filter
==================================


.. code-block:: matlab

     
    function [i_sd,i_sq,v_dc,dx] = vsc_lcl_dq(eta_d,eta_q,v_sd,v_sq,i_dc,omega,params,x)

    % parameters
    R_t = params(1);
    L_t = params(2);
    R_s = params(3);
    L_s = params(4);
    C_m = params(5);
    C_dc = params(6);

    % from the integrator to the states
    i_td = x(1);
    i_tq = x(2);
    i_sd = x(3);
    i_sq = x(4);
    v_md = x(5);
    v_mq = x(6);
    v_dc = x(7);
 
    % derivatives
    di_sd = 1/L_s*(v_md + L_s*omega*i_sq - R_s*i_sd - v_sd);
    di_sq = 1/L_s*(v_mq - L_s*omega*i_sd - R_s*i_sq - v_sq);
    dv_md = 1/C_m*(i_td - i_sd + omega*C*v_mq);
    dv_mq = 1/C_m*(i_tq - i_sq - omega*C*v_md);
    di_td = 1/L_t*(eta_d*v_dc*0.5 + L_t*omega*i_tq - R_t*i_td - v_md);
    di_tq = 1/L_t*(eta_q*v_dc*0.5 - L_t*omega*i_td - R_t*i_tq - v_mq);
    dv_dc = 1/C_dc*(i_dc - 0.75*(eta_d*i_sd + eta_q*i_sq));
    
    % from derivatives to the integrator
    dx = [di_td,di_tq,di_sd,di_sq,dv_md,dv_mq,dv_dc];



Control CTRL1 VSC 3-wire LCL-filter
-----------------------------------

.. code-block:: matlab

    function [eta_d,eta_q,dx] = ctrl_vsc(i_sd_ref,i_sq_ref,i_sd,i_sq,v_sd,v_sq,v_dc,omega,params,x)

    % parameters
    R_t = params(1);
    L_t = params(2);
    R_s = params(3);
    L_s = params(4);
    K_p = params(5);
    K_i = params(6);

    % from the integrator to the states
    xi_isd  = x(1);
    xi_isq  = x(2);


    % auxiliar
    e_isd =  i_sd_ref - i_sd;
    e_isq =  i_sq_ref - i_sq;


    % derivatives
    dxi_isd  = e_isd;
    dxi_isq  = e_isq;


    % auxiliar
    u_d = K_p*e_isd + K_i*xi_isd;
    u_q = K_p*e_isq + K_i*xi_isq;
    L = L_t + L_s;
    R = R_t + R_s;

    % outputs
    eta_d  = 2 / v_dc * ( u_d  - L * omega * i_sq  + v_sd);
    eta_q  = 2 / v_dc * ( u_q  + L * omega * i_sd  + v_sq);


    % from derivatives to the integrator
    dx = [dxi_isd,dxi_isq];



