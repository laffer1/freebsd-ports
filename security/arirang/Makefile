# Created by: Roman Shterenzon <roman@xpert.com>

PORTNAME=	arirang
PORTVERSION=	2.03
PORTREVISION=	1
PORTEPOCH=	1
CATEGORIES=	security www
MASTER_SITES=	http://monkey.org/~pilot/arirang/

MAINTAINER=	ports@FreeBSD.org
COMMENT=	Powerful webserver security scanner for network

LICENSE=	BSD3CLAUSE

LIB_DEPENDS=	libruby${RUBY_SHLIBVER}.so:${RUBY_PORT}

USES=		compiler:c11 ssl
USE_RUBY=	yes
USE_RUBY_EXTCONF=	yes

CFLAGS+=	-I${LOCALBASE}/include/ruby-${RUBY_VER} -I${LOCALBASE}/include/ruby-${RUBY_VER}/${RUBY_ARCH}
CFLAGS+=	-DRUBY_19

.include <bsd.port.pre.mk>

.if ${SSL_DEFAULT} != base
CFLAGS+=	-I${OPENSSLINC}
LDFLAGS+=	-L${OPENSSLLIB}
.endif

post-patch:
	${REINPLACE_CMD} -e 's#cc#${CC}#g' ${WRKSRC}/extconf.rb

do-install:
	${INSTALL_PROGRAM} ${WRKSRC}/arirang ${STAGEDIR}${PREFIX}/sbin
	@${MKDIR} ${STAGEDIR}${PREFIX}/share/arirang
	${INSTALL_DATA} ${WRKSRC}/scanrule/*.uxe ${STAGEDIR}${PREFIX}/share/arirang
	${INSTALL_DATA} ${WRKSRC}/script/*.rb ${STAGEDIR}${PREFIX}/share/arirang

.include <bsd.port.post.mk>
