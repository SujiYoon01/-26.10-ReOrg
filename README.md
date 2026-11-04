function remainText(end){
  if(!end) return {t:'-',soon:false};
  const v=document.getElementById('reportDate').value||new Date().toISOString().slice(0,10);
  const bp=v.split('-').map(Number), ep=end.split('-').map(Number);
  const baseT=Date.UTC(bp[0],bp[1]-1,bp[2]), endT=Date.UTC(ep[0],ep[1]-1,ep[2]);
  if(endT<=baseT) return {t:'종료',soon:false};
  const addM=k=>{ const t=new Date(Date.UTC(bp[0],bp[1]-1+k,1)); const last=new Date(Date.UTC(t.getUTCFullYear(),t.getUTCMonth()+1,0)).getUTCDate(); return Date.UTC(t.getUTCFullYear(),t.getUTCMonth(),Math.min(bp[2],last)); };
  let k=0; while(addM(k+1)<=endT) k++;
  return {t:(k===0?'1개월 미만':k+'개월'), soon:k<=3};
}
