# mysql docker解决时区差8个小时问题

总结下常见的方案：

 1.jdbc的url添加serverTimezone=Asia/Shanghai


 2.配置spring.jackson.time-zone=GMT+8


 3.mysql 设置default-time-zone=+8:00

 4.返回DTO类/添加中VO类中添加注解  
    @JsonFormat(pattern="yyyy-MM-dd HH:mm:ss",timezone="GMT+8")
    private Date createDate;

