<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FARISTRADE X — Paper Trading Terminal</title>

<style>
:root{
    --bg:#07090d;
    --panel:#0d1118;
    --panel2:#111720;
    --border:rgba(255,255,255,.08);
    --text:#f4f7fb;
    --muted:#8490a3;
    --green:#19e68c;
    --red:#ff4d67;
    --blue:#4da3ff;
    --purple:#9b6cff;
    --yellow:#ffd166;
    --shadow:0 20px 60px rgba(0,0,0,.35);
    --radius:18px;
}

*{
    box-sizing:border-box;
    margin:0;
    padding:0;
}

body{
    font-family:Inter,system-ui,-apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif;
    background:
        radial-gradient(circle at 15% 0%,rgba(77,163,255,.08),transparent 30%),
        radial-gradient(circle at 90% 10%,rgba(155,108,255,.08),transparent 30%),
        var(--bg);
    color:var(--text);
    min-height:100vh;
}

button,input,select{
    font:inherit;
}

button{
    cursor:pointer;
}

.app{
    display:flex;
    min-height:100vh;
}

/* SIDEBAR */

.sidebar{
    width:245px;
    background:rgba(8,11,16,.88);
    border-right:1px solid var(--border);
    padding:22px 15px;
    position:fixed;
    inset:0 auto 0 0;
    z-index:20;
    backdrop-filter:blur(20px);
}

.logo{
    display:flex;
    align-items:center;
    gap:11px;
    padding:8px 10px 28px;
}

.logoIcon{
    width:38px;
    height:38px;
    border-radius:12px;
    display:grid;
    place-items:center;
    background:linear-gradient(135deg,var(--blue),var(--purple));
    box-shadow:0 10px 30px rgba(77,163,255,.2);
    font-size:19px;
}

.logoText strong{
    display:block;
    font-size:15px;
    letter-spacing:.8px;
}

.logoText span{
    color:var(--muted);
    font-size:10px;
    letter-spacing:1.8px;
}

.navTitle{
    color:#596475;
    font-size:10px;
    font-weight:800;
    letter-spacing:1.5px;
    padding:0 12px 8px;
}

.nav{
    display:flex;
    flex-direction:column;
    gap:5px;
}

.nav button{
    border:0;
    background:transparent;
    color:#8994a6;
    text-align:left;
    padding:12px;
    border-radius:12px;
    transition:.2s;
}

.nav button:hover,
.nav button.active{
    background:rgba(255,255,255,.055);
    color:white;
}

.nav button.active{
    box-shadow:inset 3px 0 var(--blue);
}

.account{
    position:absolute;
    left:15px;
    right:15px;
    bottom:18px;
    padding:13px;
    border:1px solid var(--border);
    border-radius:15px;
    background:rgba(255,255,255,.025);
}

.accountTop{
    display:flex;
    justify-content:space-between;
    align-items:center;
}

.demo{
    font-size:9px;
    color:var(--green);
    background:rgba(25,230,140,.09);
    border:1px solid rgba(25,230,140,.2);
    padding:4px 7px;
    border-radius:20px;
}

.balanceSmall{
    color:var(--muted);
    font-size:11px;
    margin-top:7px;
}

/* MAIN */

.main{
    margin-left:245px;
    width:calc(100% - 245px);
    padding:22px;
}

.topbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    gap:15px;
    margin-bottom:18px;
}

.marketSelector{
    display:flex;
    align-items:center;
    gap:12px;
}

.coinLogo{
    width:46px;
    height:46px;
    border-radius:14px;
    display:grid;
    place-items:center;
    font-weight:900;
    font-size:19px;
    background:linear-gradient(135deg,#f7931a,#ffbd55);
    color:#111;
}

.coinInfo h1{
    font-size:20px;
}

.coinInfo p{
    color:var(--muted);
    font-size:11px;
    margin-top:2px;
}

select{
    background:var(--panel2);
    color:white;
    border:1px solid var(--border);
    border-radius:10px;
    padding:9px 12px;
    outline:none;
}

.topActions{
    display:flex;
    align-items:center;
    gap:8px;
}

.iconBtn{
    width:40px;
    height:40px;
    border:1px solid var(--border);
    background:var(--panel);
    color:#aab4c4;
    border-radius:11px;
}

/* STATS */

.stats{
    display:grid;
    grid-template-columns:repeat(4,1fr);
    gap:12px;
    margin-bottom:14px;
}

.card{
    background:linear-gradient(145deg,rgba(17,23,32,.96),rgba(10,14,20,.96));
    border:1px solid var(--border);
    border-radius:var(--radius);
    box-shadow:var(--shadow);
}

.stat{
    padding:17px;
}

.statLabel{
    color:var(--muted);
    font-size:11px;
    margin-bottom:8px;
}

.statValue{
    font-size:21px;
    font-weight:750;
}

.green{
    color:var(--green)!important;
}

.red{
    color:var(--red)!important;
}

.statSub{
    margin-top:5px;
    font-size:10px;
    color:var(--muted);
}

/* WORKSPACE */

.workspace{
    display:grid;
    grid-template-columns:minmax(0,1fr) 330px;
    gap:14px;
}

.chartCard{
    min-width:0;
    overflow:hidden;
}

.chartHeader{
    padding:17px 18px;
    display:flex;
    align-items:center;
    justify-content:space-between;
    border-bottom:1px solid var(--border);
}

.chartPrice{
    font-size:27px;
    font-weight:800;
}

.chartChange{
    font-size:12px;
    margin-left:8px;
}

.timeframes{
    display:flex;
    gap:3px;
}

.timeframes button{
    border:0;
    background:transparent;
    color:#687487;
    padding:7px 9px;
    border-radius:7px;
    font-size:10px;
}

.timeframes button.active,
.timeframes button:hover{
    background:rgba(255,255,255,.06);
    color:white;
}

.chartArea{
    height:430px;
    position:relative;
    padding:10px 12px 0;
}

canvas{
    width:100%;
    height:100%;
    display:block;
}

.chartBottom{
    padding:12px 18px;
    border-top:1px solid var(--border);
    display:flex;
    justify-content:space-between;
    color:#687487;
    font-size:10px;
}

/* ORDER PANEL */

.orderPanel{
    padding:17px;
}

.orderTabs{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:5px;
    background:#080b10;
    padding:4px;
    border-radius:10px;
    margin-bottom:17px;
}

.orderTabs button{
    border:0;
    background:transparent;
    color:#738096;
    padding:9px;
    border-radius:7px;
    font-weight:700;
}

.orderTabs button.active.buy{
    background:rgba(25,230,140,.13);
