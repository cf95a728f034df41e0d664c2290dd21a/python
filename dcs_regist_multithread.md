## 使用getattr省掉大段代码
```python
# /home/capric/data/yqjr/Python/trunk/dcs/regist/multithread.py
    def run(self):
        days = settings.DAYS
        now = datetime.now()

        times = datetime(now.year,now.month,now.day,0,0,0)
        pubtime = times - timedelta(days=days)
        info = RegistInfo.objects.filter(phone=self.param, pubtime__gte=pubtime)
        if len(info) >= 22:
            return
        instance = WebSite(self.param, self.order)

        axd = instance.ai_xue_dai()
        save_regist_info(**axd)

        ymd = instance.yi_ma_dai()
        save_regist_info(**ymd)

        bc = instance.bai_cai()
        save_regist_info(**bc)

        jj = instance.jiu_jiu()
        save_regist_info(**jj)

        llq = instance.ling_ling_qi()
        save_regist_info(**llq)

        pld = instance.pai_lai_dai()
        save_regist_info(**pld)

        ddh = instance.dai_dai_hong()
        save_regist_info(**ddh)

        rr = instance.ren_ren()
        save_regist_info(**rr)

        xtd = instance.xin_tong_dai()
        save_regist_info(**xtd)

        yfq = instance.you_fen_qi()
        save_regist_info(**yfq)

        mxd = instance.ming_xiao_dai()
        save_regist_info(**mxd)

        qd = instance.qu_dian()
        save_regist_info(**qd)

        ppd = instance.pai_pai_dai()
        save_regist_info(**ppd)

        by = instance.bei_yin()
        save_regist_info(**by)

        #-----------newest---------------------
        wx = instance.wo_xin()
        save_regist_info(**wx)

        # bdf = instance.bei_duo_fen()
        # save_regist_info(**bdf)

        bld = instance.bo_luo_dai()
        save_regist_info(**bld)

        lhh = instance.le_hua_hua()
        save_regist_info(**lhh)

        qdd = instance.qian_duo_duo()
        save_regist_info(**qdd)

        # sb = instance.sheng_bei()
        # save_regist_info(**sb)

        lkl = instance.la_kai_la()
        save_regist_info(**lkl)

        # lfq = instance.lai_fen_qi()
        # save_regist_info(**lfq)

        rrd = instance.ren_ren_dai()
        save_regist_info(**rrd)

        wak = instance.wo_ai_ka()
        save_regist_info(**wak)

        # nld = instance.ni_lai_dai()
        # save_regist_info(**nld)

        whd = instance.wei_huo_dai()
        save_regist_info(**whd)
```

```python
    def run(self):

        method_names = ['ai_xue_dai', 'yi_ma_dai', 'bai_cai', 'jiu_jiu']
        for name in method_names:
            method = getattr(instance, name)
            if method:
                save_regist_info(**method())
```
