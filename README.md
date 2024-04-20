# Async - Await - Promise

## Demo 2

[Check It...](https://dev-arindam-roy.github.io/Async-Await-Promise-Demo2/)

```js
const userLogin = (isApiCallOk = 1, timeTaken = 5000) => {
    let obj = {
        email: "arindam.roy.developer@gmail.com",
        password: "Test#123456",
        time: timeTaken,
        successMessage: "User Logged In Successfully"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk === 1) {
                resolve(obj);
            } else {
                reject({errorMessage: "User Login API Getting Error!"});
            }
        }, timeTaken);
    });    
}

const userProfile = (isApiCallOk = 1, timeTaken = 4000) => {
    let obj = {
        firstName: "Arindam",
        lastName: "Roy",
        email: "arindam.roy.developer@gmail.com",
        time: timeTaken,
        successMessage: "User Profile Get Successfully"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk === 1) {
                resolve(obj);
            } else {
                reject({errorMessage: "User Profile API Getting Error!"});
            }
        }, timeTaken);
    });    
}

const userAccountInfo = (isApiCallOk = 1, timeTaken = 3000) => {
    let obj = {
        accountId: "ONEX000000001",
        accountName: "Onex Developers",
        time: timeTaken,
        successMessage: "User Account Get Successfully"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk === 1) {
                resolve(obj);
            } else {
                reject({errorMessage: "User Account API Getting Error!"});
            }
        }, timeTaken);
    });    
}

const userEducation = (isApiCallOk = 1, timeTaken = 2000) => {
    let obj = {
        secondary: "Kamrabad Uchcha Vidyalaya",
        higherSecondary: "Kamrabad Uchcha Vidyalaya",
        graduation: "Sammilani Mahavidyalaya",
        master: "Future Institute Of Engineering & Management",
        time: timeTaken,
        successMessage: "User Account Get Successfully"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk === 1) {
                resolve(obj);
            } else {
                reject({errorMessage: "User Account API Getting Error!"});
            }
        }, timeTaken);
    });    
}

const userSkills = (isApiCallOk = 1, timeTaken = 1000) => {
    let obj = {
        skills: [
            {name: 'PHP', exp: '12 Years'},
            {name: 'Laravel', exp: '8 Years'},
            {name: 'Node Js', exp: '6 Years'},
            {name: 'React Js', exp: '5 Years'},
            {name: 'Vue Js', exp: '6 Years'},
            {name: 'MySQL', exp: '12 Years'},
            {name: 'MongoDB', exp: '5 Years'},
            {name: 'AWS', exp: '3 Years'},
        ],
        time: timeTaken,
        successMessage: "User Account Get Successfully"
    }
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (isApiCallOk === 1) {
                resolve(obj);
            } else {
                reject({errorMessage: "User Account API Getting Error!"});
            }
        }, timeTaken);
    });    
}

const apiCall = async (apiSettings) => {
    document.getElementById('logs').innerHTML = `Wait ${apiSettings.loginApi.time} sec`;
    document.getElementById('output').innerHTML += `<label>Response Time: ${apiSettings.loginApi.time}</label><br/>`;
    const userLoginApi = await userLogin(apiSettings.loginApi.status, apiSettings.loginApi.time).then(async (loginResponse) => {
        document.getElementById('output').innerHTML += `<label style="color: blue">User Login API</label><br/>`;
        document.getElementById('output').innerHTML += `<label style="color: green">${JSON.stringify(loginResponse)}</label><hr/>`;
        document.getElementById('logs').innerHTML = `Wait ${apiSettings.profileApi.time} sec`;
        document.getElementById('output').innerHTML += `<label>Response Time: ${apiSettings.profileApi.time}</label><br/>`;
        const userProfileAPi = await userProfile(apiSettings.profileApi.status, apiSettings.profileApi.time).then(async (profileResponse) => {
            document.getElementById('output').innerHTML += `<label style="color: blue">User Profile API</label><br/>`;
            document.getElementById('output').innerHTML += `<label style="color: green">${JSON.stringify(profileResponse)}</label><hr/>`;
            document.getElementById('logs').innerHTML = `Wait ${apiSettings.accountApi.time} sec`;
            document.getElementById('output').innerHTML += `<label>Response Time: ${apiSettings.accountApi.time}</label><br/>`;
            const userAccountApi = await userAccountInfo(apiSettings.accountApi.status, apiSettings.accountApi.time).then(async (accountResponse) => {
                document.getElementById('output').innerHTML += `<label style="color: blue">User Account API</label><br/>`;
                document.getElementById('output').innerHTML += `<label style="color: green">${JSON.stringify(accountResponse)}</label><hr/>`;
                document.getElementById('logs').innerHTML = `Wait ${apiSettings.educationApi.time} sec`;
                document.getElementById('output').innerHTML += `<label>Response Time: ${apiSettings.educationApi.time}</label><br/>`;
                const userEducationApi = userEducation(apiSettings.educationApi.status, apiSettings.educationApi.time).then(async (eduResponse) => {
                    document.getElementById('output').innerHTML += `<label style="color: blue">User Education API</label><br/>`;
                    document.getElementById('output').innerHTML += `<label style="color: green">${JSON.stringify(eduResponse)}</label><hr/>`;
                    document.getElementById('logs').innerHTML = `Wait ${apiSettings.skillApi.time} sec`;
                    document.getElementById('output').innerHTML += `<label>Response Time: ${apiSettings.skillApi.time}</label><br/>`;
                    const userSkillsApi = await userSkills(apiSettings.skillApi.status, apiSettings.skillApi.time).then((skillResponse) => {
                        document.getElementById('output').innerHTML += `<label style="color: blue">User Skill API</label><br/>`;
                        document.getElementById('output').innerHTML += `<label style="color: green">${JSON.stringify(skillResponse)}</label><hr/>`;
                        document.getElementById('logs').innerHTML = `Completed!`;
                        document.getElementById('output').innerHTML += `<label>Execution Completed!!!</label><br/>`;
                    }).catch((skillError) => {
                        document.getElementById('output').innerHTML += `<label style="color: red">${skillError.errorMessage}</label><hr/>`;
                    })
                }).catch((eduError) => {
                    document.getElementById('output').innerHTML += `<label style="color: red">${eduError.errorMessage}</label><hr/>`;
                })
            }).catch((accountError) => {
                document.getElementById('output').innerHTML += `<label style="color: red">${accountError.errorMessage}</label><hr/>`;
            })
        }).catch((profileError) => {
            document.getElementById('output').innerHTML += `<label style="color: red">${profileError.errorMessage}</label><hr/>`;
        })
    }).catch((loginError) => {
        document.getElementById('output').innerHTML += `<label style="color: red">${loginError.errorMessage}</label><hr/>`;
    }) 
}

const callApis = () => {
    document.getElementById('logs').innerHTML = '';
    document.getElementById('output').innerHTML = '';
    let loginApiTime = parseInt(document.getElementById('loginApiTime').value);
    let profileApiTime = parseInt(document.getElementById('profileApiTime').value);
    let accountApiTime = parseInt(document.getElementById('accountApiTime').value);
    let educationApiTime = parseInt(document.getElementById('educationApiTime').value);
    let skillApiTime = parseInt(document.getElementById('skillApiTime').value);

    let loginApiStatus = parseInt(document.getElementById('loginApiStatus').value);
    let profileApiStatus = parseInt(document.getElementById('profileApiStatus').value);
    let accountApiStatus = parseInt(document.getElementById('accountApiStatus').value);
    let educationApiStatus = parseInt(document.getElementById('educationApiStatus').value);
    let skillApiStatus = parseInt(document.getElementById('skillApiStatus').value);

    let settings = {
        loginApi: {time: loginApiTime, status: loginApiStatus},
        profileApi: {time: profileApiTime, status: profileApiStatus},
        accountApi: {time: accountApiTime, status: accountApiStatus},
        educationApi: {time: educationApiTime, status: educationApiStatus},
        skillApi: {time: skillApiTime, status: skillApiStatus},
    }
    console.log(settings);
    apiCall(settings);
}
```
