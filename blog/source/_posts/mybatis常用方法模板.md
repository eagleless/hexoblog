---
title: Mybatis常用方法模板
date: 2016-08-18 21:00:41
category: [database]
tags: [java,database,mybatis]
---

_常用mybatis模板批量删除、list查询、注解查询@Select。_

<!--more-->
#	根据主键集合删除
	public int delete(Object[] ids) throws Exception;
	<delete id="delete">
		delete from t_table where id in
		<foreach collection="array" index="index" item="ids" open="(" separator="," close=")">
			#{ids}
		</foreach>
	</delete>
#	根据属性值查找

	public List<T> findByList(Map<String, Object> map);
	<sql id="sample_where_clause">
		where 1=1
		<trim suffixOverrides=",">
			<if test="id !=null and id !=''">
				and id = #{id}
			</if>
			<if test="username !=null and username !=''">
				and username = #{username}
			</if>
		</trim>
	</sql>
	<select id="findByList" resultMap="BaseResultMap" parameterType="Object">
		select * from user
		<include refid="sample_where_clause" />
	</select>
#	@Select注解

	import org.apache.ibatis.annotations.Param;
	import org.apache.ibatis.annotations.Select;
	@Select("select * from work_log where id = #{id}")
	public WorkLog queryById(@Param("id")Integer id);




