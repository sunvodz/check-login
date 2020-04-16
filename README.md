# check-login

```
componentDidMount() {
// วนลูป 
setInterval(() => {
    this.handleIsExpired();
    }, 1000);
    if (!isExpired()) {

      // init ค่า ที่ใช้ ใน project แล้วแต่ ...
      this.initUser();
      this.initApp();
    }
}

// เอาไว้ check ตอน router change
  componentDidUpdate(prevProps, prevState) {
    const prevPathname = prevProps.location.pathname;
    this.handleIsExpired(prevPathname);
}


handleIsExpired() {
    const pathNotAuthen = ['/login', '/forgot-password', '/reset-password', '/access-denied'];
    let pathname = this.props.location.pathname;

    if (pathname.includes('/reset-password')) {
      pathname = '/reset-password';
    }

    const sessionExpired = isExpired();
    if (sessionExpired) {
      for (let path of pathNotAuthen) {
        if (pathname === path) return;
      }
      history.push('/login');
    }
  }



 isExpired = () => {
  let tokenInfo = getTokenInfo() 

  try{
    if( !tokenInfo  ){
      return true
    }

   if (Date.now() >= tokenInfo.exp * 1000) {
      clearTokenInfo()
      return true
    }
    return false
  } catch (e) {
    return true
  }
}
```
